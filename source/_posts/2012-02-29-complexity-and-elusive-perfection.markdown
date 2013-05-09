---
layout: post
title: "Complexity and Elusive Perfection"
date: 2012-02-29 14:15
comments: true
categories: blog op-ed
---

About three or four times a year, I find myself wishing my application wasn't so complicated.  I wish I was some stud developer who always made the right architectural decisions and didn't back myself into a corner.  I read about OO ideas regarding change management and coding for change even when you don't know what that change is and mostly, I find myself baffled.

Hindsight is 20/20.  I can see easily how the decision that seemed good at the time to make a Model.seed! method that allowed you to specify all the department data in the database AND change it in the app was a bad idea.  I can see that allowing users to change values of reports from within the reports, like a spreadsheet without using the adjustment-as-a-line-item pattern is now a bad idea... but we're 3 years on and it's just not something we're going to be able to convince the users to change or the management to invest the money in fixing.  

Then I ran across one of the <a href="https://twitter.com/#!/jeremyckahn/status/172802673853214723">best tweets ever.</a> from <a href="http://twitter.com/jeremyckahn">@jeremyckahn</a> - "All codebases are abominations. They are all terrible. If your codebase isn't a disaster, it probably doesn't do anything interesting."

It's so true.  Remembering that you'll always make some wrong choice when designing a complex app helps you to be able to cope with the pile of technical debt that has accumulated.  Making poor choices because you're lazy is one thing, but making poor choices because you don't have the experience or expertise is quite another thing entirely.

If you don't think your code is crap, you're probably doing it wrong, or you haven't been doing it long.
