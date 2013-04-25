---
layout: post
title: "TDD and Pairing Ideas"
date: 2013-04-24 10:10
comments: true
categories: 
---

When pairing, especially remotely with someone you don't work professionally with, it is sometimes helpful to have some ideas about how to go about getting the session going or what to do.  This is just a set of ideas that might get the ball rolling.

# Problems to work on

* [PuzzleNode](http://puzzlenode.com) - 15 shortish (30 minutes to 4 hour) problems.  Great for pairing.
* [Conway's Game of Life](http://coderetreat.org/gol) - Can implement a basic version quickly.  Lots of ideas for restrictions on this site.
* [TDD Katas](http://osherove.com/tdd-kata-1/) - Can be done in 30 minutes alone.
* [Dominion](http://riograndegames.com/uploads/Game/Game_278_gameRules.pdf) - A larger problem, but it will tease out larger design issues that you don't get with smaller systems.
* [Build a Twitter](http://twitter.com) - Simple system that can be extended.  Adding a UI and continuing strict TDD is very interesting since you might be able to TDD the core system, but have more difficulty with the surrounding.  Are there ways to mitigate the risks of using a framework as a shell?  Are there ways to make the shell "swappable" -- not so you'd actually swap, but so you have loose coupling?

# Ideas to practice

* [Ping Pong](http://coderetreat.org/facilitating/activities/ping-pong) - Pair back and forth, one writes a failing test, one makes it pass, then writes the next failing test, and so on.
* [Various Limitations](http://coderetreat.org/facilitating/activity-catalog) - No loops, no conditionals, limit lines per method, no voice communication (or typing out in chat... only communication is through code)
* [TDD As If You Mean It](http://cumulative-hypotheses.org/2011/08/30/tdd-as-if-you-meant-it/) - Strict TDD that involves real tests before code and strict refactoring rules.  This can be combined with any other limitation or idea, but it's so difficult (And rewarding) that it's okay to Just Do This.

# Tools

* Vim + tmux - [how to tmux](http://pivotallabs.com/how-we-use-tmux-for-remote-pair-programming/) &middot; [tmux basics screencast](http://www.youtube.com/watch?v=wKEGA8oEWXw) &middot; [Syme](https://syme.herokuapp.com/) &middot; [easy ssh/public key auth](https://github.com/chrishunt/github-auth)
* Screen Sharing - [ScreenHero](http://screenhero.com) &middot; [Google+](http://plus.google.com) (read only)
* Audio - [Skype](http://skype.com) &middot; [Google+](http://plus.google.com)
* Find Pairs - [RubyPairs](http://rubypair.com/) &middot; [IRC #pairwithme](https://kiwiirc.com/client/irc.freenode.net/pairwithme) &middot; [Twitter #pairwithme](http://pair-with-me.herokuapp.com/)
