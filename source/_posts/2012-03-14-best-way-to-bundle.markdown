---
layout: post
title: "Best Way to Bundle"
date: 2012-03-14 15:31
comments: true
categories: ruby bundler blog code
---

Thanks to the <a href="http://rubyrogues.com/045-rr-bundler-with-andre-arko/">RubyRogues Episode on Bundler</a>, I learned the best way to use bundler.

You want to always use the "pessemistic" version numbers for a handful of reasons.

```
gem 'rails', '~> 3.0.3'
gem 'rspec', '~> 2.7.0'
```

This allows the most efficient resolution of gem dependencies (in this case, any version of rails from 3.0.3 up to and not including 3.1, and any version of rspec from 2.7.0 up to and not including 2.8) and the added benefit of allowing you to easily patch everything safely using only <code>bundle update</code>.

You also want to be familiar with the various levels of 'conservatism' in updates.  

```
bundle install # once the Gemfile.lock exists... most conservative
bundle update <gem>[ <gem>] # only update specified gems
bundle update # update all gems to latest validly specified versions
```

This allows you to properly patch everything and keep your gems in proper sync in the most efficient manner.

You should also update to bundler 1.1 since it uses a much faster API call to download the latest index of gems and dependencies from rubygems.org.  Yay, faster bundler!
