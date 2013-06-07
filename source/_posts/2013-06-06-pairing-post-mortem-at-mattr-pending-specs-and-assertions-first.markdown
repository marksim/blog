---
layout: post
title: "Pairing Post Mortem - @mattr_ - Pending Specs and Assertions First"
date: 2013-06-06 13:05
comments: true
categories: blog pairing post-mortem ruby
---

Today I paired with [@mattr_](http://twitter.com/@mattr_) and got quite a bit of good input regarding how to attack a problem and write tests.  Matt is a super smart guy who has really absorbed some of the fundamentals of TDD and it shows through his ability to break down a problem.

## Setup

* TMUX & VIM on my box
* Conway's Game of Life as an exercise

## Process 

When [implementing the game of life](https://gist.github.com/marksim/5723610), we started off looking at the problem on Wikipedia and found the 4 rules.  I immediately started writing the first test when Matt noted that he liked to write all the specs he knows of as pending specs right at the beginning.  Then he can really plow forward and know what's next.  He also noted that he likes to be able to write the assertion first, based on the test, and then build the test up from there.  I felt the lightbulb go off when he pointed these two things out.  When I've struggled to find the test or figure out how to test something, usually it's because I can't figure out how to get to the assertion, and that really comes down to not testing the right thing.

After talking through those points, we went through the TDD process for the Cells and moved on to the actual Game (interaction of Cells).  Things got interesting here since we started noticing how divorced our Cells were from our Game itself.  We decided we wanted to use a Graph of cells to really implement the game when we ran out of time.  It was great to see how the tests were pointing us towards the problems in our code.

## Takeaways

* Write as many pending specs as you can first
* Write your assertions first
* ???
* Unicorns and Rainbows.

Looking forward to pairing with [@mattr_](http://twitter.com/@mattr_) again.  He was very knowledgable and good to work with.

On to the next pairing session...
