---
layout: post
title: "Pairing Post Mortem - @hinbody - Attacking Open Source is Hard"
date: 2013-06-14 10:47
comments: true
categories: blog pairing post-mortem oss
---

The easiest things to pair on are little tasks that you both understand and can be easily "completed" within a 1-2 hour pairing session.  Unfortunately, Tic Tac Toe, Conway's Game of Life and Bowling become stale quickly.  It's not that they don't have valuable things to teach you, but you can't pair with the same people over and over again just doing those problems.  Eventually you need to dive into a real project.

At that point, you have two options:

1. Work on a project one of you is authoring
    - Open Source Gem (widely accepted)
    - Closed Source (some people feel as though they should be paid for working on a commercial product)
2. Work on an Open Source project with the goal of submitting a pull request.

The second option is more viable for most of the pairing community.  Not everyone will have an OSS project they feel is worth pairing on, and not everyone can get permission to let a random pair work on their closed source project.  Even with those two options crossed off, you can also both learn by reading other code and solving other people's issues.

In my latest pairing with [@hinbody](http://twitter.com/hinbody), we tried our hand at [Spree](https://github.com/spree/spree) and learned a few things along the way.  

## Observations

We started off by looking at Spree's issues and trying to select one that looked like somewhat low hanging fruit

* It was hard to find low hanging fruit.
* Pull-requests mixed in with the issues made it more difficult to find what we wanted.
* Lack of familiarity with the product probably multiplied the difficulty.

After we finally found what looked like a very simple documation change, we dug in a bit.

* We wanted to see code work that indicated what the documentation *should* be, so we tried to get the tests to work.
* Most of our pairing time was spent trying to get the environment set up so that we could run specs.  
* The issue and comments did not seem to match what we saw in the code.

## Takeaways

* Having the code you're going to work on checked out and tests running/passing saves a lot of time.
* Picking an issue is hard.  [Being familiar with the project/domain](/blog/2013/05/16/pairing-post-mortem-at-kmeister2000/) makes a big difference.
* Picking an issue is part of the learning process.  Just digging in to figure out what an issue was talking about gave us a better feeling about that specific part of the project.

Not the most productive pairing session, but still worthwhile because we learned a bit about how to begin digging into Open Source

On to the next pairing session...
