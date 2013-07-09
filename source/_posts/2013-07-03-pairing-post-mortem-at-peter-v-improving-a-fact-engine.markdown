---
layout: post
title: "Pairing Post Mortem - @peter_v - Improving a Semantic Store"
date: 2013-07-03 10:03
comments: true
categories: blog pairing post-mortem ruby
---

Today I got to pair with [Peter Vanderabeele](http://twitter.com/peter_v), who is a programmer from Belgium with a highly methodical bent.  He has clearly had a lot of experience and it was neat to get to work on his project since it isn't every day you get to work on a high performance fact storage system. 

Peter is creating a data store meant to store semantic facts that have relationships to each other.  It's a very different project with a goal, he stated, to have data in this format and extractable for the next 50 years.  To try to view code with that lens is very different from how most other Rubyists think.  We tend to see our code dying in the next 5 years... max.  So we make decisions with that timeline in mind.  Thinking of a timeline longer than my own life has very different implications.

Pretty much all my sessions these days are VIM+TMUX. ScreenHero is useful for when someone else doesn't have everything set up, but in general, TMUX+VIM is the way to go.  I set up our session and cloned [his project](https://github.com/petervandenabeele/dbd).  The tests all passed after a quick <code>bundle</code> and so we were ready to go.

Once we got to coding, one thing I really liked was being able to just <code>Ack</code> for the <code>TODO</code> comments.  We found 2 in the codebase and talked about both of them.  One seemed fairly simple and a good way to get introduced to the project, so we went with it.  We wanted to validate that the format of a CSV coming in was good on a row-by-row basis.  

We started by discussing how to *describe* the correct formats for each column.  Eventually [we converted the array of attributes](https://github.com/petervandenabeele/dbd/pull/3/files) to a hash of attributes and [regexs](http://rubular.com/).  That made it easy to loop through the parsed CSV and determine if each field was valid.  It was easy to make each of these changes because the tests were fairly thorough and so every change made at least a handful of tests fail.  We would see the failing tests, make the appropriate modifications, and then watch everything pass.  Man, I love a project with a great test suite.

We also quickly determined, once we saw some tests failing after we expected them to pass, that we neglected the idea that some fields were optional.  We added an additional flag to the hash, which is when we should have refactored to a <code>ColumnSpec</code> class, but we didn't quite have the time.  Either way, we got the tests passing and saw the validation working as we had expected.

## Takeaways

* <code>TODO</code>s in code are very useful for pairing and figuring out what to attack, even more so than an Issue tracker, I believe.
* Thorough tests made it very, very easy to make changes with confidence.
* US Lunchtime pairings work well for most EU evening pairers :)
* Goals and timelines for your project have significant effects on your willingness to compromise.  It's important to know what you're trying to do and how long you are trying to do it. 

All in all, I learned quite a bit from pairing with Peter and I hope we get to do it again soon.

On to the next pairing session...

