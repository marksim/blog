---
layout: post
title: "Pairing Post Mortem - @kmeister2000 - Refactoring and MiniTest"
date: 2013-05-29 22:19
comments: true
categories: ruby pairing post-mortem blog
---

Had a great 4th pairing with [@kmeister2000](http://twitter.com/kmeister2000).  Always a pleasure to work with him.

**Interesting Parts of our session setup:**

* Worked on a real world app Karl was developing
* Used MiniTest instead of RSpec
* Refactored existing code

**MiniTest Takeaways:**

* MiniTest expectations about method calls are not as clear as in Rspec and the documentation/examples aren't as readily available.
* MiniTest is a lot like RSpec in nearly every other way.
* I'm not a fan of Mocha.  I think it promotes antipatterns for how to really test.
* I actually like the explicit <code>mock.verify</code> in MiniTest::Spec

**General Takeaways:**

* Real world stuff is hard.
* Naming is hard.
* The testing drove us to better design, even if the test [wasn't pretty](https://gist.github.com/kmeister2000/311d1287a0caf6e21b5a).  We still ended up with a wrapper class for the external Stripe API and converted a <code>before_save</code> callback to a decorator class that delegated appropriately.
* Being unfamiliar with tools is the biggest time suck when you're working.  High proficiency lets you actually get things done.  Low proficiency means you're learning the tool more than solving the problem.
* Corrollary: Learn tools on problems you know.  Solve problems on tools you know.
