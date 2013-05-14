---
layout: post
title: "Ping Pong Pairing without Screen Sharing"
date: 2013-05-09 11:09
comments: true
categories: blog pairing
---

I often have a bit of time that I could spend on other tasks, but couldn't set up a true share-and-pair session due to logistics and communication issues.  A friend of mine suggested that we "pair" over github.  I took the idea to the next level by creating a true ping-pong pairing project where each commit is a ping or a pong.

Here's the basic setup:

1. Create a README with the full description of the "task" at hand
2. Create a github repo and [add your 'pair' as a collaborator](https://help.github.com/articles/how-do-i-add-a-collaborator).
3. Write a failing spec
4. <code>git commit</code> and <code>git push</code>

Then, each individual takes turns doing the following:

1. Get a tweet/alert/message/email... whatever... from your pair
1. <code>git pull</code>
2. Run the specs and see the failing one
3. Write code until it passes
4. Write a spec that fails based on the README
5. <code>git commit</code> and <code>git push</code>
6. Tweet/alert/message/email your pair (maybe github notifications will work?)

Basic **benefits** are : Zero setup, no need to learn other editor, a full commit history for every single step, no need to coordinate schedules.

Clear **drawbacks** are : No immediate guidance, less pushing out of comfort zone, less intensity, slower

It's not the same as pairing since you're not letting the discussion and 2 sets of eyeballs help, but it's a lot like the [mute pairing session](http://coderetreat.org/facilitating/activity-catalog) Corey Haines talks about at Code Retreats.  I'm interested to see where it will go.  Maybe it could even go towards a "round robin" implementation?  (i.e 3 or more collaborators?).  Check out our [little experiment on GitHub](http://github.com/marksim/dominion) to see how it goes. 
