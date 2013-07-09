---
layout: post
title: "Pairing Post Mortem - @stuartrexking - Cane Extension"
date: 2013-06-24 15:09
comments: true
categories: blog pairing post-mortem ruby
---

Last night's pair session was with [@stuartrexking](http://twitter.com/stuartrexking) - a very experienced developer and technologist currently working at a really neat company called [Antipodean Labs](http://antipodeanlabs.com/).  It seems like he's got a great handle on solving problems and staying maintainable.

We started off by trying to decide what to do.  I'm increasingly convinced this is the possibly the hardest part of remote pairing with people who aren't part of your company.  You don't have a predefined complex project you both find interest in, so the most likely shared interests are either meta problems or highly common ones.  Highly common ones are very visible and difficult to find low hanging fruit for.  The meta problems are good to solve, but somehow feel like they are less valuable than the "real" problems.  Maybe this is just a feeling I have.

We eventually decided to make an extension to [Cane](https://github.com/square/cane) to count the number of lines in a method.  We started off by writing an acceptance test, which turned out to be much easier than the implementation.  Once we got that test running, we started running into problems with Cane's architecture.  Cane doesn't pass in a file to a "filter", but rather requires that you parse a glob yourself.  This seems like it doesn't scale well.  Running into this problem made us rethink our position entirely and by that point, I was a bit too tired and worn out from other things that happened this week.  We put our project on hold and decided to come back to it next time.

I still have takeaways from this session, even though by most accounts we wouldn't consider it a "success" in terms of producing something or completing a task.

## Takeaways

* I like writing an acceptance test that "wraps" a bunch of unit testing.  The unit tests end up driving your coding decisions and the acceptance test makes sure you're driving toward the feature you intended.
    - Acceptance test says 'this is my finished feature in a black box'
    - Unit tests drive individual methods and behaviors and decisions to ge that acceptance test to pass.
* Deciding on a project is probably best outside of the context of the pairing.  Shoot ideas back and forth prior to so little time is wasted once you're "on" and ready to pair.
* <code>:bp</code> in VIM rotates to the previous buffer.  Nice.
* Pairing with people much brighter than myself makes me want to improve.  YMMV, but I'd encourage you to *try* to think that way, even if it's unnatural at first.

I really enjoyed pairing with Stuart and hope we get to finish up our project soon.  Looking foward to more time with him in the near future.

On to the next pairing session...
