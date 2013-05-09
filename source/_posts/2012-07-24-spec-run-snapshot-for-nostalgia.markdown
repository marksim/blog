---
layout: post
title: "Spec Run snapshot--for nostalgia"
date: 2012-07-24 15:53
comments: true
categories: blog nostalgia test
---

I thought it would be interesting to take a snapshot of a full, timed spec run every month or so and post it.  Who knows, sometime I might look at this and think "13.7 seconds!  THAT'S FOREVER" -- Or I might look at it and say "13.7 seconds!  I Wish!"

I also have been pushing to improve the coverage by 1% ever 2-3 days (That's roughly 10-20 additional covered lines).  My goal is to get to 85% and stop.  Lots of stuff doesn't need to be tested and lots of stuff is "covered" but not actually tested properly.  Testing is hard.

``` bash Rspec
time be rspec spec --tag ~slow
Run options: exclude {:slow=>true}
...........................................................................................................................................................................................

Finished in 4.61 seconds
187 examples, 0 failures
Coverage report generated for RSpec to /Users/marksim/dev/reqhub/reqhub/coverage. 1082 / 1502 LOC (72.04%) covered.

real     0m13.772s
```
