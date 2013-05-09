---
layout: post
title: "DCI Generators in Rails"
date: 2012-05-22 12:10
comments: true
categories: dci rails blog code ruby
---

Recently, in my new project, I decided to take the [DCI](http://en.wikipedia.org/wiki/Data,_context_and_interaction) approach that [Mike Pack outlined](http://mikepackdev.com/blog_posts/24-the-right-way-to-code-dci-in-ruby), which has been really cool.  I've been able to keep my tests fast, and have very distinct buckets to put data (models), specific roles of that data (rather than cluttering up the models), and an easy way to take a use case and map it out programatically (contexts).  

I noticed that I was generating roles and contexts regularly and copying from previously written code examples so I decided to make role and context generators.  The process wasn't bad, but it did take a couple of steps that took a little digging to understand.

My Role generator pretty much just generates this:
``` ruby my_role.rb
module MyRole
end
```

But it also hooks into RSpec and generates this
``` ruby my_role_spec.rb
require 'fast_spec_helper'
require 'staffing_professional'

class TestMyRole; end

describe MyRole do
  let(:subject) {
    s = TestMyRole.new
    s.extend MyRole
  }
  pending "add some specs to my_role_spec.rb"
end
```

The generator itself is pretty easy to setup... Rails even has a generator for making a generator!

``` bash
$ rails g generator role
      create  lib/generators/role
      create  lib/generators/role/roles_generator.rb
      create  lib/generators/role/USAGE
      create  lib/generators/role/templates
```

The important file there is <code>roles_generator.rb</code>

``` ruby roles_generator.rb
class RoleGenerator < Rails::Generators::NamedBase
  source_root File.expand_path('../templates', __FILE__)
end
```

What's going on here?  Well, the digging came in for Rails::Generators::NamedBase, which provides a bunch of fun little helpers like <code>file_name</code>, <code>class_name</code>, <code>singular_name</code>, <code>plural_name</code> etc -- and this is exactly what you want when you're making a generator for something like Roles or Contexts.  

So I expanded the roles_generator:
``` ruby rails_generator.rb
class RoleGenerator < Rails::Generators::NamedBase
  source_root File.expand_path('../templates', __FILE__)

  def generate_role
    empty_directory 'app/roles'
    template 'role.rb', File.join('app/roles', class_path, "#{file_name}.rb")
  end

  hook_for :test_framework
end
```

It doesn't matter what you call the method... every public method gets called. I don't even want to know the horrid magic that had to go on to make that happen just the way they wanted it to.  There are a bunch of fun helpers you can call like <code>copy_file</code>, <code>exists_dir</code>, and <code>template</code> which give you most of what you need.  Lots of other help is available in the [<code>Thor::Actions</code> docs](http://textmate.rubyforge.org/thor/Thor/Actions.html)

It was pretty easy to set up the templates at that point. 

``` ruby templates/role.rb
module <%= class_name %>
end
```

You'll also notice the little <code>hook_for :test_framework</code> line at the bottom of the generator.  That enables you to tie into whatever test framework you've configured, which means this could be easily packaged up as a gem with support for both <code>Rspec</code> and <code>Test::Unit</code> depending on what you wanted to use.

Adding the support for Rspec was pretty easy, but you're tapping into rspecs generators if you want to do it right, not just copying files willy nilly within your own generator.

I added a directory called <code>lib/generators/rspec</code> that included <code>roles_generator.rb</code> and a templates directory

The generator looks like this:
``` ruby rspec/roles_generator.rb
module Rspec
  # Generates a spec file for the role module
  class RoleGenerator < ::Rails::Generators::NamedBase
    source_root File.expand_path('../templates', __FILE__)

    def build_role_specs
      empty_directory 'spec/roles'
      template 'role_spec.rb', "spec/roles/#{singular_name}_spec.rb"
    end
  end
end
```

Only thing to note here is the <code>module Rspec</code> that wraps the whole class.  Without this, Rspec won't pick up the generator.

Then make your spec template

``` ruby rspec/templates/role_spec.rb
require 'fast_spec_helper'
require '<%= singular_name %>'

<%= "class Test#{class_name}; end" %>

describe <%= class_name %> do
  let(:subject) {
    s = Test<%= class_name %>.new
    s.extend <%= class_name %>
  }
  pending "add some tests to the <%= file_name %>_spec.rb"
end
```

Since it's a module, we set up a test class that is automatically extended as <code>subject</code> since any other use of <code>subject</code> doesn't make sense.

Easy cheesy!  

Now I just need to extract these generators to a <code>dci_generators</code> gem :)
