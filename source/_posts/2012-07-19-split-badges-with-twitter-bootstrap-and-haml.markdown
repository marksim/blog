---
layout: post
title: "Split Badges with Twitter Bootstrap and HAML"
date: 2012-07-19 08:21
comments: true
categories: css blog haml code
---

I recently needed to display a few contextual numbers near each other in a web app.  I've taken to liking the twitter bootstrap 'badges' for little informational numbers, especially with the color coding that <code>badge-important</code>, <code>badge-info</code>, and <code>badge-success</code> provide.  Easy ways to quickly communicate not only the number, but a hint at what it means.

The problem is that when you put a bunch of badges right next to each other, you get kindof a mess.

{% img /images/badge-messy.png Messy Badges %}

So I went looking for 'split badges' (or some such thing), which I've seen on various applications, notibly on 'Things':

{% img /images/badge-example.png Example Badges %}

But I couldn't find anything that just 'told' me how to do it, or put it in a plugin... or anything.  So I set out to just make it happen.

I'm using [rails](http://rubyonrails.org) and [twitter bootstrap](http://twitter.github.com/bootstrap/index.html), so I threw this in bootstrap_and_overrides.css.less

``` css bootstrap_and_overrides.css.less
.badge-right {
  -webkit-border-top-left-radius: 0px;
  -moz-border-top-left-radius: 0px;
  border-top-left-radius: 0px;
  -webkit-border-bottom-left-radius: 0px;
  -moz-border-bottom-left-radius: 0px;
  border-bottom-left-radius: 0px;
  margin-left:0px;
  padding-left:5px;
}

.badge-left {
  -webkit-border-top-right-radius: 0px;
  -moz-border-top-right-radius: 0px;
  border-top-right-radius: 0px;
  -webkit-border-bottom-right-radius: 0px;
  -moz-border-bottom-right-radius: 0px;
  border-bottom-right-radius: 0px;
  margin-right:0px;
  padding-right:5px;
}

.badge-middle {
  -webkit-border-radius: 0px;
  -moz-border-radius: 0px;
  border-radius: 0px;
  margin-right:0px;
  margin-left:0px;
  padding-right:5px;
  padding-left:5px;
}
```

``` haml show.html.haml
Vendors
&nbsp;
%span.badge.badge-success.badge-left= accepted_count
%span.badge.badge-info.badge-middle= pending_count
%span.badge.badge-important.badge-right= rejected_count
```

Then I went to implement them and noticed the gaps.

{% img /images/badge-gaps.png Clean, gaping Badges %}

Since I was using [HAML](http://haml.info), the spans automatically had spaces inserted around them.  Hmmmm...

Apparently all it takes is a little <code>&gt;</code> to tell HAML to behave.

``` haml show.html.haml
Vendors
&nbsp;
%span.badge.badge-success.badge-left>= accepted_count
%span.badge.badge-info.badge-middle>= pending_count
%span.badge.badge-important.badge-right>= rejected_count
```

And we have what we want!  Yay for clean badges!

{% img /images/badge-clean.png Cleaner Badges %}
