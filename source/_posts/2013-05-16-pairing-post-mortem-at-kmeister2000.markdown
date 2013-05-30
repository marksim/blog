---
layout: post
title: "Pairing Post Mortem - @kmeister2000 - TDD and Domain Knowledge"
date: 2013-05-16 10:07
comments: true
categories: blog pairing post-mortem tdd 
---

Last night I did a [#pairwithme](http://pairprogramwith.me) session with Karl Meisterheim.  He's an experienced developer who currently work part time and was looking to improve his skills.  Besides having a good deal in common and really enjoying our conversation, I also learned a bit more about remote pairing and came away with a couple of observations.

First off, we paired 2 nights in a row for about an hour each night.  Both sessions we tried to solve the same problem:  TicTacToe.  We started off on the second night with the code from the first night, but quickly threw it away and decided to "start over" as an excercise.  Doing this taught me the most significant lessons from our session.

[The code from the first night](https://gist.github.com/kmeister2000/5581429) ended up heading in a direction we didn't really like.  It wasn't horrible, but it wasn't something we felt confident in.  I learned about Sublime's Vintage mode (a very nice way to pair with someone where one is used to VIM and one is used to TextMate/Sublime!) and I experienced ScreenHero from the client side.  I still have the same observations about it as I did at my other pairing session:  great product for a super fast, no fuss setup.

So the second night, we threw the code away and [started again](https://gist.github.com/marksim/5592334).  Doing that gave us the lessons we learned from the other code without being tied to our former implementation.  We went in a completely different direction, summed up nicely in an observation Karl made: "TDD is no substitue for lack of domain knowledge."  When we struggled the night before, it was mostly because we didn't have a clear idea of what we wanted to implement.  Taking just a few minutes and writing down comments that described the properties of a TicTacToe game made a great deal of difference.  This has been referred to more 'formally' as [README driven development](http://tom.preston-werner.com/2010/08/23/readme-driven-development.html).  Write your README first and make your specs off of that... then your code off your specs.

As programmers, we are often translators between English (or your native tongue) and 'Computerese' (in whatever flavor you subscribe).  Taking the time to make small steps between the words you speak and the code you write is part of being a good developer.

All in all, a great experience with Mr. Meisterheim!  Hope to do it again on a more 'real-world' problem next time.
