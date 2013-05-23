---
layout: post
title: "Testing Complex Queries in Rails"
date: 2013-05-14 16:52
comments: true
published: false
categories: sql tdd rails ruby blog
---

Rails extracts out a lot of ways to avoid all sorts of SQL.  This means that we often don't have to handle big, complex queries.  But inevitably, we will one day have a report to write, or an algorithm to run that needs significant SQL.  Since the advent of 'fast tests' it's often said that you should stub out database access, but that should only really be true at the points where you're testing how your app works with DATA from the db, not when you're testing how SQL commands are executed.

This means that the only effective way to TDD complex SQL is to actually set up test data and make assertions about it.

In this post, I want to walk through testing a query that does the following:

**Given a set of users who have a history of orders, write a query to return 'suggestions' for items the user might be most likely to buy**

It's a complex query.  It's something you could do in AREL or straight SQL, but either way you need to TDD it since you have real problems you're trying to solve.  If you want to work with the predictive data, then stub that out in other tests so you don't get the performance hit, but all tests related to this need to hit the database.

First, we'll be doing this in a new

``` bash Generate Models
rails new sqltdd -d postgresql
echo "group :development, :test do" >> Gemfile
echo "  gem 'rspec-rails'" >> Gemfile
echo "  gem 'factory_girl_rails'" >> Gemfile
echo "end"  >> Gemfile
bundle
rake db:create # You may need to modify your user in config/database.yml
rails g rspec:install
rails g model User name:string
rails g model Order user:references
rails g model Item name:string
rails g model OrderItem item:references order:references
```

Note that there would be many more properties for each object in a real scenario, this is mostly an exercise in 'complex' data queries, so we've stripped it down to be the simplest version of complex that makes sense.

We'll go ahead and add the appropriate <code>has_many</code> references to <code>User</code>, <code>Order</code> and <code>Item</code> and remove the pending specs generated for us there.  We're not testing how these classes work individually... that can be done outside the database, we're testing a query class that interacts with all of them.

Let's start from the top down and write a test like this:

``` ruby SuggestedItemsQuery spec
describe SuggestedItemsQuery do
  it "returns items suggested for a given user" do
    query = SuggestedItemsQuery.new(Item.active)
    ted_mosby = FactoryGirl.create(:user)
    first_order = FactoryGirl.create(:order)
    ted_mosby.orders << first_order
    first_order.items << FactoryGirl.create(:item, name: 'yellow umbrella')
    first_order.items << FactoryGirl.create(:item, name: 'bass guitar')
    
    query.items_for(ted_mosby).pluck(:name).should include "ticket to farhampton"
  end
end
```

This test is ugly, though, and it's difficult to see what's going on.  Let's factor out the creation of a user with orders and items so it's easier to see what's happening in a given test.

``` ruby SuggestedItemsQuery spec
describe SuggestedItemsQuery do
  def user_with_items(name, orders=[])
    user = FactoryGirl.create(:user, name: name)
    user.orders = orders.each do |items|
      order = FactoryGirl.create(:order, user: user)
      items.map do |item_name|
        FactoryGirl.create(:item, name: item_name)
      end.each do |item|
        order.items << item 
      end
    end
    user
  end

  it "returns items suggested for a given user" do
    query = SuggestedItemsQuery.new(Item.active)
    ted_mosby = user_with_items("Ted Mosby", [["blue french horn", "yellow umbrella", "bass guitar", "boots"]])
    
    query.items_for(ted_mosby).pluck(:name).should include "ticket to farhampton"
  end
end
```

Now we have a readable test that makes it clear what we're creating and how.  Notice how we can encapsulate all of the pieces of the data that don't matter to the test inside FactoryGirl or the helper method.  This way when you add a required field in orders, you're not having to rewrite 30 tests.  

But we're still not done with this test.  We have an assertion based on some assuptions about the data IN the database.  This is where understanding the fundamental difference between the data present and the data specific to a given test is critical.  We want to create a 'sea' of data we run tests against that is relatively large and unchanging, and then create little bits of data that mimic specific users in each test.  The thing that will derail this type of test driven development quickly is trying to reconstruct your "sea" every time.

Let's use our new helper method to create our sea.

``` ruby Creating the 'Sea of Data'
describe SuggestedItemsQuery do
  def user_with_items(name, orders=[])
    # ...
  end

  before(:all) do
    # User with nothing in common
    user_with_items("Marshal Eriksen", [['slap bet game', 'ticket to italy', 'king kong costume']]

    # User with one item in common in one order
    user_with_items("Lily Aldrin", [['boots', 'diapers', 'expensive art']]

    # User with many items in common
    user_with_items("Robin Scherbatsky", [["blue french horn", "boots", "gun"]]

    # User with many items in common
    user_with_items("The Mother", [['yellow umbrella', 'bass guitar'], ['boots', 'ticket to farhampton']])
  end

  it "..."
end
```

Since we're using the <code>before(:all)</code> hook rather than <code>before(:each)</code>, we get the benefit of only setting this thing up once.  Awesome.  Now we have a fully set up test that we can begin to drive toward the features of our query.
