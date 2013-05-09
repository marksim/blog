---
layout: post
title: "Running Rails 3.2 on a shared Dreamhost with Passenger"
date: 2012-07-20 12:59
comments: true
categories: hosting rails blog code deployment
---

*Update:* While it's good to understand what you're doing, [this template file](https://gist.github.com/4658117) will get you so that after you get your app running, <code>cap deploy:setup</code> and <code>cap deploy:cold</code> works, assuming you have the host set up properly and have your app's main directory cleared of all files.  

## Everybody Loves Dreamhost, but...

Dreamhost is a great little hosting company, but it really lags when it comes to keeping the latest software up to date. It's version of Ruby is 1.8.7 and the latest stable version of Rails they have running is 3.0.3.  That release is technically in "security fix" mode.  Ugh.

So I'd like to run Rails 3.2, but don't want to pay for a VPS since this system is going to be small and simple.  How can I do it?

As it turns out, it's relatively easy.  I only ran into one headache and was able to install anything I wanted without any problems.  How did I do this?  The secret, my friends, is <code>bundle pack</code>

## Creating a new Vendored App

Let's create a new Rails 3.2 app and set our local RVM to use 1.8.7 since that's what passenger uses (and can't use another version)

``` bash Terminal
$ rails new myproject -d mysql
...
$ cd myproject
$ echo "rvm use 1.8.7" > .rvmrc
$ cd ../myproject # to engage the new rvmrc
$ echo "gem 'capistrano'" >> Gemfile
$ bundle install
$ bundle package
$ capify .
```

## Deploying via Copy

Now you'll need to edit your deploy file.  It's easy to deploy via copy:

``` ruby config/deploy.rb 
require 'bundler/capistrano'

# to get past the 'bundle not installed errors'
set :default_environment, {                                                     
  "PATH" => "~/.gems/bin:/usr/lib/ruby/gems/1.8/bin/:/usr/local/bin:/usr/bin:/bin:"
}                                                                               
set :shell, "/bin/bash"   
 
set :application, "myproject"

set :scm, :none
set :repository, "."
set :deploy_via, :copy

set :domain, MY_DREAMHOST_DOMAIN
set :user, MY_DREAMHOST_USER
set :deploy_to, "/home/#{user}/#{application}/"
set :use_sudo, false

role :web, domain
role :app, domain
role :db,  domain, :primary => true # This is where Rails migrations will run

# if you want to clean up old releases on each deploy uncomment this:
after "deploy:restart", "deploy:cleanup"

# If you are using Passenger mod_rails uncomment this:
namespace :deploy do
  task :start do ; end
  task :stop do ; end
  task :restart, :roles => :app, :except => { :no_release => true } do
    run "#{try_sudo} touch #{File.join(current_path,'tmp','restart.txt')}"
  end
end
```

Make sure you set up your config/database.yml to include your production database connection data and let's do a deploy

``` bash Terminal
$ cap deploy:setup
$ cap deploy:cold
```

## The Big Gotcha: The Asset Pipeline

Now we need to enable the asset pipeline.  First uncomment the line related to it in <code>Capfile</code>

``` ruby Capfile
load 'deploy'
# Uncomment if you are using Rails' asset pipeline
load 'deploy/assets'
load 'config/deploy' # remove this line to skip loading any of the default tasks
```

### ... and multiple platform hell.

Then we need to handle the singular headache that is related to the asset pipeline if you're working on a different platform than Debian linux (say, OS X)

The libv8 gem that is installed and vendored on your local cache is for 'darwin', which is not compatible with the linux architecture.  I looked to see if I could figure another way around this, but the best way I could find is to ssh in, uncomment <code>gem 'therubyracer'</code> and run <code>bundle update && bundle pack</code> on the remote box.  Then I copied the <code>libv8-3.3.10.4-x86_64-linux.gem</code> file in <code>vendor/cache</code> down to my local vendor cache and went on my merry way.

After that, you can <code>cap deploy</code> to your hearts content and you'll have a fully deployed Rails 3.2 app on the shared Dreamhost running through passenger!
