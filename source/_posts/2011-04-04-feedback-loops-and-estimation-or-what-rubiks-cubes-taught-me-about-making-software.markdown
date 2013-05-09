---
layout: post
title: Feedback Loops and Estimation -or- What Rubik's Cubes Taught Me About Making
  Software
categories: blog op-ed
---
Estimation is hard.  It may not be listed as one of the top <a href="http://laughingmeme.org/2005/12/23/there-are-only-two-hard-things-in-computer-science-cache-invalidation-and-naming-things/">two problems in computer science</a>, but it's at least a close third. Over the years I've gotten to try all sorts of methodologies for estimating.  Waterfall, Agile, Points, Stories, Requirements, Features, Epics, Pomodoros, Billable hours... you can go on forever with the Jargon of Management, trying to get information from a developer about how much longer The Client has to wait until The Feature is finished.
## Rubik's Cubes
About 4 years ago I started a job where a coworker was an avid Rubik's cube solver.  I learned the steps and began competing with him to see who could solve a cube the fastest.  Eventually, my top time ended up around a minute and thirty seconds.  There are guys who can <a href="http://www.youtube.com/watch?v=zLQJ93B5Nl0">do</a> <a href="http://www.youtube.com/watch?v=bm6ohS55Tu0">it</a> <a href="http://www.youtube.com/watch?v=uBqaOs6omrI">much faster</a>--but I'm interested in consistency and improved speed.  Sometimes I can solve very quickly because some steps can be skipped (i.e. they are done for you) or because I'm using a very good cube, but in general, I can solve a cube in 1:30 - 3:00.

But I don't <a href="http://www.youtube.com/watch?v=JCkI2qh1SF4">do it blindfolded</a>.
## Blindfolded
The world record for the fastest solve is just under 10 seconds, but the world record for the fastest blindfold solve (i.e. from the time you pick it up, look it over, and then blindfold yourself to begin solving) is over a minute and a half--10 times as long.  The reason is simple--<strong>feedback</strong>.  Immediate and quick feedback allow you to take shortcuts and spend less time worrying about the next 200 moves and just worry about the next step or two.

So why do we still tend toward "blindfolded" approaches in software?
## Waterfall vs. a Feedback loop
Call it Agile, call it scrum, call it feedback--it doesn't matter.  What makes a team think they're going to deliver better because they took the time to figure out all the steps, when you don't know exactly how one step will affect the next?  It's foolish when you consider it, but still, so many teams do it.  Even the supposed "agile" teams end up blindfolding releases and then trying to 'feedback' the sprints.  That's not to say there should be no planning, but getting customer and developer feedback is crucial to accurate and fast solutions to problems.

What should we be doing instead?  In Rubik's Cube solutions, you typically identify the next 'step' and iterate over it, examining the result and deciding the following step at that point.  You might be able to 'blindfold' for each step, but you'd still need to look at the end to figure out where to go next.  I think a similar paradigm works in software building.  Identify the key feature, and let the developer work on it, deploy it, and get feedback.  Iterate on it again if it's not quite right.  If it is, then move along to the next step or feature.
## Analogy Breakdown
Where does this analogy break down?  Architectural changes.  You can't make sweeping changes underneath the system without a good deal of planning and "blindfolding" where you step through, unsure of the effect on the system because you can't actually evaluate it. There are times this must occur--but as developers, we probably tend toward a desire to rearchitect more often than we should.  Always consider what the right solution is and evaluate the cost of technical debt vs. the <strong>potential cost</strong> of an underlying change that could have pervasive and unknown effects.  Sometimes it is necessary, but generally it's not.  <a href="http://www.google.com/url?sa=t&amp;source=web&amp;cd=1&amp;ved=0CCIQFjAA&amp;url=http%3A%2F%2Fen.wikipedia.org%2Fwiki%2FYou_ain't_gonna_need_it&amp;ei=0ACaTeScFc3Htwe0mJnuCw&amp;usg=AFQjCNHaDCOVQWLpBfX1NqScK8nJ-kZ8FQ">YAGNI</a> is your friend.
## Takeaway
The tighter the feedback loop, the more accurate and more quickly you're able to deliver a solution, whether in Rubik's world or in the Software space.  Focus on tight loops with customer feedback <em>and</em> developer feedback and watch your estimation troubles diminish.
