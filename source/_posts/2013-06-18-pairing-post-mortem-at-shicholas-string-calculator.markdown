---
layout: post
title: "Pairing Post Mortem - @Shicholas - String Calculator"
date: 2013-06-18 16:17
comments: true
categories: blog pairing post-mortem ruby
---

Last night I had a great pairing with [@Shicholas](http://twitter.com/Schicholas) working on the [String Calculator kata](http://osherove.com/tdd-kata-1/).  

## Setup

We again used TMUX + VIM, even though Nick wasn't very familiar with VIM.  Based on his experience, I think this might be the **best way to learn VIM** since you have someone guiding you through.  You won't pick up on everything, but you'll learn a handful of new things each time.

## Exercise

[We went through each of the different rules and ping ponged back and forth](https://gist.github.com/marksim/5802445).  It was a struggle to do the *simplest* possible thing every time, and really let the tests DRIVE your development.  Your developer brain wants to generalize the solution to a problem, but the strength of TDD is keeping your *actual* solution as simple as possible.  Developers are notorious for over complicating things and over desigining.

We found that refactoring for readability vs. duplication/maintainability was in conflict.  Specifically when we needed to split a string to look for a delimiter and then keep the remainder to parse later.  We could have put that code in an initializer, or a helper--but we would have either divorced the implementation from where it was used or made redundent calls.  We opted for redundent calls until it became a problem.

## Takeaways

* **The strength of TDD is keeping your solution as simple as possible**
* Refactoring is really dealing with tradeoffs and trying to figure out the best way given a set of circumstances.  It's an art not a science.
* It's easy to teach/learn VIM when you're pairing as long as people have a basic understanding of Insert/Command mode
* Ruby 2.0 has this thing called [refinements](http://pivotallabs.com/failed-attempt-at-trying-to-use-refinements/) that [sound like a good idea](http://yehudakatz.com/2010/11/30/ruby-2-0-refinements-in-practice/), but [probably aren't ready for prime time yet](http://rubyrogues.com/099-rr-ruby-2/).  We didn't experiment with them... I just found out about them because we did a tiny monkey patch of String for the exercise.

I'm really starting to see how powerful real TDD is, especially in the context of pairing.  I hope I can see this further as the pairings I participate in go past exercises and onto real world stuff.  I'm excited to see how much my TDD improves.

On to the next pairing session...

