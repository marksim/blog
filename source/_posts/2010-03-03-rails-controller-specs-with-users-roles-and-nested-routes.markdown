---
layout: post
title: Rails Controller Specs with users, roles and nested routes
categories: blog rails code rspec tdd
---
I've long put off testing my controllers because of user authentication and nested controllers, dealing with stubs, etc.

But today, a fully working test!  

As background, Advertisers have many trackers and the routes look like this:
``` ruby config/routes.rb
ActionController::Routing::Routes.draw do |map|
  map.resources :advertisers do |advertisers|
    advertisers.resources :trackers
  end
end
```

To set everything up in the specs, I included all the files in the spec/support directory and used <a href="http://mocha.rubyforge.org/">Mocha</a> as my mock framework
``` ruby spec/spec_helper.rb
Dir[File.expand_path(File.join(File.dirname(__FILE__),'support','**','*.rb'))].each {|f| require f}

Spec::Runner.configure do |config|
  config.mock_with :mocha
end
```

Then I set up my factories (<a href="http://railscasts.com/episodes/158-factories-not-fixtures">rather than fixtures</a>) using <a href="http://github.com/thoughtbot/factory_girl">Factory Girl</a>

``` ruby spec/factories.rb
Factory.define :user do |user|
  user.sequence(:login) { |n| "username#{n}" }
  user.password 'password'
  user.password_confirmation { |u| u.password }
  user.sequence(:email) { |n| "email#{n}@example.com" }
  user.first_name "Mama"
  user.last_name "Foo"
end

Factory.define :advertiser do |advertiser|
  advertiser.name 'Advertiser 1'
end

Factory.define :tracker do |tracker|
  tracker.name 'Tracker 1'
end
```

Now we get down to brass tacks.  In order to make my tests DRY (appropriately) and allow for all my controllers to test if someone is logged in and has access, I set up this shared context
``` ruby spec/support/user_authentication.rb
describe "an admin is logged in", :shared => true do
  before(:each) do
    controller.stubs( :login_required => true)
    controller.stubs( :current_user => Factory.build(:user, :login => 'admin', :roles_list => ["super"]))
  end
end
```

From there, all we need to do is put it all together, setting up trackers parent @advertiser and the @tracker we'll be using and stubbing the ActiveRecord find so that it always returns @advertiser
``` ruby spec/controllers/trackers_controller.rb
describe TrackersController do
  it_should_behave_like "an admin is logged in"
  integrate_views
  
  before(:each) do
    @advertiser = Factory.create(:advertiser)
    @tracker = @advertiser.trackers.create(Factory.attributes_for(:tracker))
    Advertiser.stubs(:find => @advertiser)
  end
```
  
Now we simply specify the part of the path that is needed to find the nested route by using :advertiser_id => @advertiser
``` ruby spec/controllers/trackers_controller.rb
  it "index action should render index template" do
    get :index, :advertiser_id => @advertiser
    response.should render_template(:index)
  end
  
  it "show action should render show template" do
    get :show, :advertiser_id => @advertiser, :id => @tracker
    response.should render_template(:show)
  end
  
  it "new action should render new template" do
    get :new, :advertiser_id => @advertiser
    response.should render_template(:new)
  end

  it "create action should render new template when model is invalid" do
    Tracker.any_instance.stubs(:valid?).returns(false)
    post :create, :advertiser_id => @advertiser
    response.should render_template(:new)
  end

  it "create action should redirect when model is valid" do
    Tracker.any_instance.stubs(:valid?).returns(true)
    post :create, :advertiser_id => @advertiser
    response.should redirect_to(advertiser_tracker_url(@advertiser, assigns[:tracker]))
  end
  
  it "edit action should render edit template" do
    get :edit, :advertiser_id => @advertiser, :id => @tracker
    response.should render_template(:edit)
  end
  
  it "update action should render edit template when model is invalid" do
    Tracker.any_instance.stubs(:valid?).returns(false)
    put :update, :advertiser_id => @advertiser, :id => @tracker
    response.should render_template(:edit)
  end
  
  it "update action should redirect when model is valid" do
    Tracker.any_instance.stubs(:valid?).returns(true)
    put :update, :advertiser_id => @advertiser, :id => @tracker
    response.should redirect_to(advertiser_tracker_url(@advertiser, assigns[:tracker]))
  end
  
  it "destroy action should destroy model and redirect to index action" do
    delete :destroy, :advertiser_id => @advertiser, :id => @tracker
    response.should redirect_to(advertiser_trackers_url(@advertiser))
    Tracker.exists?(@tracker.id).should be_false
  end
end
```

Works!   And works great!   A minimal and excellent way to test your controllers, especially for access.  You can easily create additional shared contexts with different user permissions and extend out the tests to make sure users that don't have access can properly access them.
