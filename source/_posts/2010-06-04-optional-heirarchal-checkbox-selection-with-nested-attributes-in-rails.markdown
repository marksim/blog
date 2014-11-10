---
layout: post
title: Optional Heirarchal Checkbox Selection with Nested Attributes in Rails
categories: blog rails ruby code
---
I had a process where I wanted users to fill out a survey which had hierarchal categories AND be able to specify some additional data for specific capabilities that the user had.

<a href="/images/Screen-shot-2010-06-04-at-2.11.01-PM.png"><img src="/images/Screen-shot-2010-06-04-at-2.11.01-PM.png" alt="" title="Categories Example" width="260" height="276" class="alignnone size-full wp-image-73" /></a>

Now, you could easily do this for a small subset and hand-code every item, but I wanted a flexible survey system that allowed true hierarchy and generalized code.

Let's start off with the basic survey and capabilities models and relationships:

``` bash
./script/generate model Survey name:string
```

``` ruby app/models/survey.rb
class Survey < ActiveRecord::Base
  has_many :survey_capabilities
  has_many :capabilities, :through => :survey_capabilities
end
```

``` bash
./script/generate model Capability name:string parent_id:integer question:string
```
``` ruby app/models/capability.rb
class Capability < ActiveRecord::Base
  has_many :survey_capabilities
  
  belongs_to :parent, :class_name => 'Capability'
  has_many :capabilities, :foreign_key => 'parent_id'
end 
```

``` bash
./script/generate model SurveyCapability survey:references capability:references answer:string
```

``` ruby app/models/survey_capability.rb
class SurveyCapability < ActiveRecord::Base
  belongs_to :survey
  belongs_to :capability
end
```

Your first attempt at making a survey map to many capabilities will be something like this (formtastic):
``` ruby
<%= f.input :capabilities, :as => :check_boxes %>
``` 

But while that works on a basic level, it doesn't work for capabilities that have a hierarchy and it doesn't allow the user to specify additional data (i.e. answer a question about the capability).

So we're going to need to accept nested resources.   So we add this line to survey.rb:
``` ruby
accepts_nested_attributes_for :site_capabilities, :reject_if => lambda { |a| a[:capability_id].blank? || a[:capability_id].to_i == 0}, :allow_destroy => true
```

Now we need to recursively display hierarchal capabilities (If you show videos on your site, you might allow the user to invoke it, or require the user to invoke it, but if you don't show videos, we don't care about your invocation restrictions):

First, let's make a quick way to show/hide enable/disable elements within a div:
``` javascript public/javascripts/application.js
function toggle_fields(element_id, value) {
  if (!value) {
    Effect.SlideUp(element_id, { duration: 0.1 })
  }
  $(element_id).select('input').each(function(element) {if (value) { element.enable() } else { element.disable() }})
  $(element_id).select('select').each(function(element) {if (value) { element.enable() } else { element.disable() }})
  $(element_id).select('textarea').each(function(element) {if (value) { element.enable() } else { element.disable() }})
  if (value) {
    Effect.SlideDown(element_id, { duration: 0.1 })
  }
}
```

Now let's create a helper that will set up the capabilities checkboxes and nested inputs:
``` ruby app/helpers/survey_helper.rb
def select_capabilities(f, collection)
    html = ""
    collection.each do |capability|
      survey_capability = f.object.survey_capabilities.select{|obj| obj.capability_id == capability.id}.first
      selected = !!survey_capability
      survey_capability ||= f.object.survey_capabilities.build(:capability_id => capability.id)
      f.fields_for :survey_capabilities, survey_capability  do |cap_form|
        html += cap_form.input :capability_id, :as => :boolean, :label => capability.name, 
          :input_html => {:onclick => "toggle_fields('capability_#{capability.id}_details', this.checked);$('capability_#{capability.id}_delete').value = (!this.checked ? '1' : '0')"},
          :checked => selected, :checked_value => capability.id
        html += cap_form.input :_delete, :as => :hidden, :value => "0", :id => "capability_#{capability.id}_delete"
        html += content_tag :div, (capability.question.blank? ? "" : cap_form.input(:answer, :label => capability.question)) + (capability.capabilities.any? ? select_capabilities(f, capability.capabilities) : ""), {
            :id => "capability_#{capability.id}_details", :class => "details",
            :style => "display:#{selected ? "block" : "none"}"
        } if capability.capabilities.any? || !capability.question.blank?
      end
    end
    html
  end
```

There is a lot going on here.   Let's step through.

Keep in mind that we're recursive, so first off, we're passing in the collection of Capabilities we're dealing with through the "collection" parameter, but that isn't what we need to create in terms of nested form attributes--we need SurveyCapability objects for that, so we have to find or build them:

``` ruby
      survey_capability = f.object.survey_capabilities.select{|obj| obj.capability_id == capability.id}.first
      selected = !!survey_capability
      survey_capability ||= f.object.survey_capabilities.build(:capability_id => capability.id)
```

Then we create the fields_for section for nested form attributes and pass in the SurveyCapability we just created.   Since we can specify that we want checkboxes here and specify the value, we make the checkbox the capability_id and make sure the 'checked_value' is the capability.id (it is '1' by default).

``` ruby
  html += cap_form.input :capability_id, :as => :boolean, :label => capability.name, 
                :checked => selected, :checked_value => capability.id
```

And while we're at it, we'll create a way to remove the relationship altogether if they uncheck the capability
``` ruby
   html += cap_form.input :_delete, :as => :hidden, :value => "0", :id => "capability_#{capability.id}_delete"
```

Finally, we build up the optional sub-question in the case of a click:
``` ruby
  html += content_tag :div, (capability.question.blank? ? "" : cap_form.input(:answer, :label => capability.question)) + (capability.capabilities.any? ? select_capabilities(f, capability.capabilities) : ""), {
            :id => "capability_#{capability.id}_details", :class => "details",
            :style => "display:#{selected ? "block" : "none"}"
        } if capability.capabilities.any? || !capability.question.blank?
```

And now we can add the :onclick option to the original checkbox so that appropriate inputs are toggled on click:
``` ruby
   :input_html => {:onclick => "toggle_fields('capability_#{capability.id}_details', this.checked);$('capability_#{capability.id}_delete').value = (!this.checked ? '1' : '0')"},
```

After we've got all that going on, we simply have to place it in the _form view:
``` ruby app/views/surveys/_form.erb
<% semantic_form_for @survey do |f| %>
  <%= select_capabilities f, Capability.find(:all, :conditions => {:parent_id => nil}) %>
<% end %>
```

Instead of doing Capability.find..., let's add a named scope to the Capability class:
``` ruby app/models/capability.rb
class Capability
  named_scope :top_level, :conditions => {:parent_id => nil}
  ...
end
```

Yeah!  Now you don't have to change your controllers at all and you can have optional, hierarchal selection of checkboxes with nested attributes!
