---
layout: post
title: ! 'Code Kata #1 - Supermarket Pricing'
categories: blog ruby code
---
Taken from <a href="http://codekata.pragprog.com/2007/01/code_kata_one_s.html">Code Kata's by Dave Thomas</a>

The basic premise of this Kata is asking how you would model super market pricing.  What is the price of an item?  What is the cost?  How do you handle price-per-pound?  Buy 2 get one free?  What's the value of stock? It's interesting, and I thought I'd take the time to blog through my thought process.

I'd like to iterate over the design and see where it takes me.  First task is to represent a product.
``` ruby
    class Product
      attr_accessor :name
      attr_accessor :price
      attr_accessor :quantity

      def initialize(name, quantity, price)
        @name = name
        @quantity = quantity
        @price = price
      end
    end
```
Basic enough... But the :price element can't simply be a float... no it's it's own object... let's look at that closer
``` ruby
    class Price
      attr_accessor :amount
      attr_accessor :unit # nil, :pound, :oz, :box, etc
      attr_accessor :multiple # defaults to 1, enables '3 {units} per {amount}'
      attr_accessor :num_free # defaults to 0, enables 'buy {special} get 10 free!'
      attr_accessor :special # defaults to nil, enables 'buy 3 get {num_free}'

      def initialize(params={})
        params.each {|p,v| send("#{p}=", v)}
      end
    end
```

At first, this looks overly complicated, but it allows us to store the exact input and calculate off of that.  We never want to store $0.3333333 / orange when the user enters 3 for $1--that would make our rounding happens at the EARLIEST possible moment, rather than the latest.  We also want to enable flexible definitions of what costs the amount specified, thus you could say 0.99/pound, etc.  There should be some units that are known, and others that are simply treated the same a nil (or /each).  I'm not thrilled with the num_free or special yet... maybe those will factor themselves differently as we go forward.

So what can we represent here... let's set up some examples:
``` ruby
    apple = Product.new "apples", 200, Price.new(:amount => 1.99, :unit => :pound)
    soup  = Product.new "soup", 100, Price.new(:amount => 1.00, :multiple => 3)
    oreos = Product.new "oreos", 50, Price.new(:special => 4, :num_free => 1, :amount => 2.98)
    bread = Product.new "bread", 25, Price.new(:amount => 1.69)
```
There's a couple things about these that I want to refactor as I'm going... I want the price to be a bit more readable... like:
``` ruby
    apple = Product.new 200, "apple", :at => 1.99, :per => :pound
    soup  = Product.new 100, "chicken noodle soup", :at => 1.00, :for => 3
    oreos = Product.new 50,  "oreos", :at => 2.98, :buy => 4, :get => 1
    bread = Product.new 25,  "bread", :at => 1.69, :per => :loaf 
```
That's what I'd like.  It reads straight across.  You can represent most things here... so we'll refactor "Price" and "Product" to look like that:
``` ruby
    class Product
      attr_accessor :name
      attr_accessor :price
      attr_accessor :quantity

      def initialize(quantity, name, price)
        @name = name
        @quantity = quantity
        @price = price.is_a?(Hash) ? Price.new(price) : price
      end
    end
```
``` ruby
    class Price
      attr_accessor :at
      attr_accessor :per # nil, :pound, :oz, :box, etc
      attr_accessor :for # defaults to 1, enables '{for} {per} per {at}'
      attr_accessor :get # defaults to 0, enables 'buy {buy} get {get} free!'
      attr_accessor :buy # defaults to nil, enables 'buy {buy} get {get}'

      def initialize(params={})
        params.each {|p,v| send("#{p}=", v)}
      end
    end
```
There!  Much better!  Now how about being able to call "cost" for a specific quantity of something. Should it be on the "product" or the "price"?  They are closely related, but the product is what needs the call, most likely delegating some of the calculation to the price.  Let's set up "Price.of(n)" and "Product.buy!(n)"  Product.buy!(n) will actually decrease the quantity we have in stock.
``` ruby
class Price
  # ...
  def of(quantity, unit=:each)
    quantity = convert(quantity, unit)
    (quantity / for) * @at
  end
end

class Product
  def buy!(n)
    @quantity -= n
    price.of(n)
  end
end
```
This continues to be tougher and tougher, but I'm getting the idea.  This would be great for a TDD driven exercise.  I'd like to do the timed Kata like Corey Heines does -- to music even :)  

Enough for this Kata.  Time to move on to Kata #2.
