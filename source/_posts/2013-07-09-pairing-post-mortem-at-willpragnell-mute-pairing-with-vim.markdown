---
layout: post
title: "Pairing Post Mortem - @willpragnell - Mute Pairing with VIM"
date: 2013-07-09 09:35
comments: true
categories: blog pairing post-mortem ruby games vim
---

Last week I had the opportunity to pair again with [@willpragnell](http://twitter.com/willpragnell).  He had just moved and didn't have internet access, so I suggested that we try a "mute" pairing session from a coffee shop, where all our communication happened through VIM.

He was game, so we started off with a quick chat session on Google+ to get set up, and then switched to a VIM+TMUX setup for the rest of the time.

## Observations

* It was nice to listen to music during pairing since I normally listen to music while coding
* It required a bit more thinking since we sometimes began typing over one another.  Wasn't a big deal, just something I became aware of.
* We used comments to "talk out" our ideas
* It was faster to get going since we didn't spend a lot of time gabbing at the beginning.

We began working on an engine for the game [Pandemic](http://www.amazon.com/Z-Man-Games-7021ZMG-Pandemic/dp/B0013OBXG2).  We realized that trying to implement the whole game would be a bit to much to bite off in one session, so we decided on trying to get the map/graph parts of the game going along with the ability to know what the infection state was at any given location.

When we started by trying to define a location that knew about all it's neighbors, we quickly realized that wasn't the best way to represent it and went for more of a Graph form, with points and edges.  The points knew information specific to them (infection level, research station status), but didn't know about it's neighbors, that was the board's job.

We also worked a bit on refactoring and naming towards the end.  One of the biggest plusses of pairing is that you can bounce ideas off each other related to naming so that you really communicate in the best possible ways to future maintainers.

After about 45 minutes, we made a good deal of progress and I think we're ready to begin implementing the city decks and all the rules related to them next time around.  It was quite fun.

## Takeaways

* Mute pairing sessions aren't as fluid as sessions with audio, but they do in a pinch.
* Implementing a game is really fun since there are lots of different things to consider, but the ruleset is still finite.
* Implementing a game that deals with geography with someone overseas is humorous.
* Refactoring naming alone is a huge benefit of pairing.  I would have stuck with <code>cure</code> and <code>partial_cure</code> for method names, but considering that the default needs to be partial cures, we changed to <code>cure</code> and <code>cure_all</code> -- much better, I think.

Can't wait to make more progress on the game.  Looking forward to pairing with Will again.

On to the next pairing session...
