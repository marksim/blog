---
layout: post
title: "CanCan and Devise with nil current_user on POST"
date: 2012-04-11 13:07
comments: true
categories: blog rails code
---

I had a Rails 2.3.X app that I migrated to Rails 3.  When I did, I upgraded CanCan and Devise.  Suddenly, my delete links weren't working.  I remembered that unobtrusive JS was the default so I hopped into the <code>application.html.erb</code> template and added the relevant javascript tags.

``` ruby application.html.erb
  ...
  <head>
    ...
    <%= javascript_include_tag 'prototype', 'rails', 'application' %>
    ...
  </head>
...
```

Great!  Now my delete links weren't just links to the show action, but when I did click them I noticed that a CanCan error appeared.  After some debug statements, it became clear that <code>current_user</code> wasn't set, but only on the POST/DELETE methods.  Hmmm.  What could be causing this?

Yes!  The csrf tags!

If you're upgrading to Rails 3 and you see odd behavior on POSTs with the session (anything that tries to protect_from_forgery), make sure you have this line in the head section of your application layout.

``` ruby
  <%= csrf_meta_tag %>
```

Crisis, averted.
