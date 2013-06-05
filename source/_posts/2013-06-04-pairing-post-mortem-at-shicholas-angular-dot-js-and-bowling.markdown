---
layout: post
title: "Pairing Post Mortem - @Shicholas - Real World Lessons and Bowling"
date: 2013-06-04 15:37
comments: true
categories: blog post-mortem pairing ruby
---

Last night I had my first pairing session with [@shicholas](http://twitter.com/shicholas).  Nick recently graduated from law school and is looking to pass the bar, but somehow programming calls to him.  It's a good thing too, since he's clearly gifted and a fast learner.

Setup:

* ScreenHero
* Sublime Text 2
* [shuhari](https://github.com/jarhart/shuhari) by [@jarhart](http://twitter.com/jarhart)

While we were kicking things off with the "get to know you" talk, I found that Nick had a Rails + [Angular.js](http://angularjs.org/) app he was working on.  I've not done any work with Angular and asked him to show me what was going on.  He pointed out the general structure as well as the custom *directives* that Angular.js allows you to create.  I've watched the [Ember.js Peepcode Intro](https://peepcode.com/products/emberjs), and found it difficult to get excited about it.  Being introduced to Angular.js in this particular manner gave me real world applications and it seemed much more intriguing.  No verdict yet on either, just initial impressions on both frameworks.

After a few minutes looking at Angular, we decided to implementing the Bowling Scoring as a quick TDD exercise in Ruby.  We used [shuhari](https://github.com/jarhart/shuhari) to set up the app and have everything in place for quick exercise.  It's a nifty little gem for speeding up the setup process if you're wanting to focus on learning something specific.

[We got through the whole exercise](https://gist.github.com/shicholas/5703467) in about 45 minutes.  I'm discovering that Test Driven Development is affected a great deal by the intuitions you have about where something is heading.  Implementing the "minimum solution" to pass the test is often subjective.  Gary Bernhardt said in one of his Destroy All Software screencasts that there was a point where he could code the constant as a return value to make the test pass, but it was actually much less mental effort to solve it outright, so he did.  There was no test that forced him there, he just did it.  It made the test pass, and certain other tests didn't have to be written.  We saw this happen in our last 2 tests because of the way we chose to iterate over "frames" in the bowling score implementation.

Takeaways:

* Be open to learning about what other people are doing.  Their real world applications show you much more than any exercise will ever show you.
* Angular.js looks more exciting than I'd initially thought.
* [shuhari](https://github.com/jarhart/shuhari) is a cool tool for pairing on basic exercises.
* Be aware of how much you blur the line between letting tests drive your design and using your intuition to discover the next step.

It was a great session and I am hoping that I get to pair with Nick again on his Angular.js project.  

On to the next pairing session...
