---
layout: post
title: "Pairing Post Mortem - @willpragnell - Overseas TDD"
date: 2013-06-14 17:19
comments: true
categories: blog pairing post-mortem ruby
---

I had my first pairing session with [@willpragnell](http://twitter.com/willpragnell) today.  He's a smart guy and my first European pair partner.  It was a pleasure to talk to him about his iOS and Ruby experience and I picked up on a lot of little things from our pairing session together.

## Setup

* TMUX and VIM - (I got to use my [newly revised pairing script](https://gist.github.com/marksim/5785406) to set up everything in seconds)
* TicTacToe - RSpec 

## The Session
We set a couple of goals out for the beginning.  We both wanted to learn more of RSpec's new syntax and we wanted to really adhear to the TDD principle of doing the most simple thing next.

We spent about 45 minutes [implementing TicTacToe](https://gist.github.com/marksim/5785703) and came up with a different implementation than I've ever done before. One of the reasons was that we started off by writing our [pending specs first](/blog/2013/06/06/pairing-post-mortem-at-mattr-pending-specs-and-assertions-first/) and we had a lot of discussion for HOW to solve the problem.  TDD is the least brittle and most helpful when you focus on what something does rather than worrying about how it does it.  Oddly, this is difficult sometimes to agree on.  Does Tic Tac Toe, the game, alternate players, or is that just how people play it?  Making these kinds of decisions with your tests makes a difference in how you implement.

## Takeaways

* Think a lot about your tests: they shape your design, so **badly designed tests probably result in bad design.**
* It made a difference in how we were going to design the tests when we decided this was going to be a shell for a UI.  **Think of how your code will be consumed**
* I like RSpecs new syntax, especially since it doesn't pollute the object method space: <code>expect(game.play(5)).to be_true</code>
* <code><c-x><c-l></code> in vim autocompletes a whole line 
* There is nothing like pairing to make you realize how much every developer loves to cusomize their editor/environment.

Great session!  I look forwarding to my next with [@willpragnell](http://twitter.com/willpragnell)

**UPDATE** - *afterwards, I really liked where this was going.  I spent a little time and tried to finish out the implementation.  [It's my favorite implementation of TicTacToe because it's so simple.](https://gist.github.com/marksim/5786740)  Thinking of the UI, but coding the tests just under it made it easy to drive and then super simple to throw on a CLI that worked perfectly.*

On to the next pairing session...
