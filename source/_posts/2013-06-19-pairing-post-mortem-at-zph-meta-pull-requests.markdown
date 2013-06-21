---
layout: post
title: "Pairing Post Mortem - @_zph - Meta Pull Requests"
date: 2013-06-19 15:58
comments: true
categories: blog pairing post-mortem ruby
---

I had a great [#pairwithme](http://pairprogramwith.me) session with [@_zph](http://twitter.com/_zph).  Always a pleasure to talk to him and solve a problem together.

## Setup

* TMUX + VIM on a slice
* [github-auth](https://github.com/chrishunt/github-auth) gem

## Experience

We wanted to add the feature to <code>gh-auth</code> so you could pass a <code>--path</code> or <code>--user</code> argument to it.  Because we're good developers, we started off by coding the acceptance test.  We discussed the merits of how to write good tests and whether to follow convetions within a gem authored by someone else or do things 'the right way' -- according to whatever coding religion you follow.  Eventually we decided on sticking to the conventions of the gem while trying to improve--but not radically change--the tests/testing that we touched.  From there, we dove down into the implementation and unit tests and drove through until we had the <code>--path</code> argument working.  Along the way we did a little refactoring to use the [OptionParser](http://ruby-doc.org/stdlib-1.9.3/libdoc/optparse/rdoc/OptionParser.html) instead of requiring a specific ordering of options.

Within an hour and a half we had successfully test driven a new feature and gotten it working.  We aliased <code>--user</code> to basically be a shortcut for <code>--path</code>, but that was it.

## Takeaways

* Solving real problems teaches you very different things than solving exercises.
* A good test suite is crucial for getting people to be able to contribute to your library
* Convention should probably trump your coding religion in 90% of the cases.  As with any religion, introduce it in small pieces when it comes up.
* Having a [near ready pull-request](https://github.com/zph/github-auth/commit/7f306ce6bc1c9567872dfc037dc237f3a1bc7215) to show for a pairing session felt amazing.
* <code>OptionParser</code> is *very* useful.

I am looking forward to more and more OSS contributions through pairing. I'm almost thinking I need to 'invent' a widly useful (not necessarily *used*) gem to be able to pull out when I'm pairing to get the maximum effect.  Super cool.

On to the next pairing session...
