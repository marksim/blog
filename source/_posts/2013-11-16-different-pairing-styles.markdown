---
layout: post
title: "Different Pairing Styles"
date: 2013-11-16 21:42
comments: true
categories: blog pairing op-ed
---

Pairing is hard, but to me, the hardest part about remote pairing is not technology or even logistics, it's collaboration and problem solving together.  To that end, there are multiple pairing styles that are worth looking at when you're trying to pair with someone knew.  Each style facilitates collaboration differently and knowing how they work helps.

# Driver / Navigator

**Fundamental Idea**
One partner "drives" at the keyboard, focusing on implementing. The other partner "navigates" verbally, focusing on big ideas, questions, typos, and conventions.

**Strengths** 

* Great for "unequal" pairing partners / mentoring (let the less experienced 'drive')
* Let's someone with a highly customized environment work effectively without inhibiting the navigator
* Great for "thinking through" big problems you're solving.
* Easy tech setup, can just use screen share.

**Weaknesses**

* Can lend itself toward one partner becoming less engaged (Driver is only copying what is said, Navigator stops talking)
* Equal partners may desire more "take turns" kind of approach
* Driver learns less tech, navigator learns less theory/big ideas
* Weaker on TDD, small problems, repetitive solutions


# Trade off / Taking Turns

**Fundamental Idea**
Partners take turns driving and navigating, perhaps with a 15-20 minute timer.

**Strengths**

* Both partners get to learn tech and think about big ideas
* Keeps both partners engaged
* Great for partners of similar skill levels
* Still good for thinking through problems
* *Can* sync code via git to allow for current driver to use their own environment.

**Weaknesses**

* Hard if host environment is unfamiliar for either pair
* Harder to "mentor", but still a viable option


# Ping-pong

**Fundamental Idea**
Partners take turns by making all tests pass, writing a failing spec and passing control to the other partner.

**Strengths**

* Great for exercises
* Keeps both partners engaged
* OK for mentoring or more equal pairing

**Weaknesses**

* Really difficult in unfamiliar environment
* Nearly requires a terminal sharing/buffer sharing style of pairing
* Bad for big problems, communication is most effective through tests, easy to psych yourself out otherwise.

# Conclusion

Which pair style you pick will be up to you and your pairing partner, but it's worth considering what kind of problem you have and what your relationship is with your partner.    My general rule of thumb is, for small exercises, do Ping-Pong pairing.  For real world problems with unequal skill levels, do Driver-Navigator with the less experienced person driving.  For real world problems with equal skill levels, trade off to keep things interesting.  YMMV.

