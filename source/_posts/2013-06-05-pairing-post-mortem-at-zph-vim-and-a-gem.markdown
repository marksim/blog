---
layout: post
title: "Pairing Post Mortem - @_zph - VIM and a Gem"
date: 2013-06-05 10:55
comments: true
categories: blog pairing post-mortem ruby vim
---

Last night I had a great [#pairwithme](http://pairprogramwith.me) session with [@_zph](http://twitter.com/_zph).  He's been doing Ruby on nights and weekends for the last few years and he's been using [VIM](http://www.vim.org) much longer than I have.  I learned a lot of little tricks about VIM that I just hadn't quite worked out before.  We also refactored some of his [Buff](http://github.com/zph/buff) Gem.

Setup:

* Zander had a VPS already provisioned with my ssh keys installed.  Super Easy setup.
* TMUX + VIM for our editors
* RSpec for testing the Gem

We started off trying to think of what to pair on within Zander's gem. He was concerned about the tests, so we actually spent a fair amount of time just looking at the WebMocked tests and discussing the pros and cons.  Eventually we decided that WebMock might be a good way to start off your TDD of an API wrapper since you have complete control of the response, but VCR gives you the best long term support since you can both get fast tests and confirm that you're still working with the API correctly and that you didn't just magically stub out the wrong thing--just delete your cassette and you've got "free" real API tests, followed by nice fast tests.

Just having this discussion was valuable.  We didn't change any code since Zander felt it would mostly be tedious and he wanted to do it himself.  I can't decide if that's a great use of pair time or a 'wrong' feeling that some things aren't worth pairing on.  Either way, our time talking about pros and cons of testing styles was one of my favorite moments.

We eventually [refactored his url encoding](https://github.com/zph/buff/commit/c7431cb8df6e37bb52667fd822464380068f85a0) to isolate a few things and make some of the methods query methods rather than query-command mixes.  I introduced him to <code>Enumerator#with_index</code> as well.  In the process of doing this I saw how proficient Zander was at VIM.  He showed me the [vim-surround](https://github.com/tpope/vim-surround) plugin, the [vim-numbertoggle](https://github.com/jeffkreeftmeijer/vim-numbertoggle) plugin, and the [vim-ruby-refactoring](https://github.com/ecomba/vim-ruby-refactoring) plugin.  I hadn't really seen any of them in action.  I think the refactoring plugin needs to have a bit more to it, but relative numbers really seemed like a great idea.  I also learned little things like <code>Shift-j</code> to join the next line to this one and <code>viw</code> to select a whole word.  I'd always selected whole lines and yanked whole lines.  Learn something new every day.

Takeaways:

* Discussion is one of the most valuable things about any pairing session.  Bouncing ideas off is where you change the way you actually think.
* Learning tools from other people is just as valuable as improving code.
* Things I take for granted are easy to forget to point out.  I knew about <code>with_index</code> and thought nothing of it.  He didn't know you could chain that off of any enumerator.  Ah... the value af other people's brains.

All in all, a great session.  Looking forward to the next one with [@_zph](http://twitter.com/_zph).

On to the next pairing session...
