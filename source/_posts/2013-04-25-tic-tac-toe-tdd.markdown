---
layout: post
title: "Tic Tac Toe TDD"
date: 2013-04-25 10:26
comments: true
categories: blog ruby tdd code
---

I spent a little (longer than I thought... maybe 2 hours?) implementing Tic-Tac-Toe in the TDD As If You Mean It style.  Ended up with a VERY different implementation than I ever would have done if I just "started coding" -- everything was only in one class, including the AI to "play" against itself.

<script src="https://gist.github.com/marksim/5460578.js"></script>

Observations:

* It was quite different to implement things inside the test method.  I ended up coding like

{% codeblock %}
it "does something..." do
  player = Player.new

  def player.something
    # do work
  end

  player.something.should be_true
end
{% endcodeblock %}

* It was difficult to not refactor as I went.  Many times I would see the duplication and want to refactor immediately.  I resisted this urge until I felt the implementation was done, then refactored out duplication, ensuring that the tests continued to pass after each change.
* I'm still not quite sure how you're supposed to improve design without breaking the rules. Doing pure method move seems limiting and doesn't allow for you to see duplication.  The only thing I could think of is that there can be additional refactoring after you're "done"

All in all, a very interesting exercise.  I want to do it now on something broader, and eventually on something that has a core with a wrapper so that the core is purely TDD'd and the wrapper is thin, but swappable.  I think Dominion is my next big attempt. 
