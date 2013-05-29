---
layout: post
title: "Pairing Post Mortem : @thecommongeek - Ruby Koans"
date: 2013-05-28 12:17
comments: true
categories: ruby pairing post-mortem code
---

I paired with [@thecommongeek](http://twitter.com/thecommongeek) last night again.  This time we were more prepared and I think the session went much better.

In our [first session](/blog/2013/05/13/pairing-as-mentoring-first-impressions/) I misjudged where Dennis was as a coder and struggled a bit with how to pair with him effectively.  This time we had him drive through [ScreenHero](http://screenhero.com) and decided to start from the "basics" by doing the [RubyKoans](http://rubykoans.com).  

The RubyKoans are meant for Ruby 1.8.7, but 1.9.3 is commonplace now, so we struggled a bit at the beginning.  For anyone going through the RubyKoans on 1.9.3 getting a <code>value19</code> in nearly all your errors, I'd suggest making the following changes on neo.rb (starting on line 34):

``` ruby neo.rb
def __
  if RUBY_VERSION < "1.9"
    value
  else
    :blank_value
  end
end

# Numeric replacement value.
def _n_
  if RUBY_VERSION < "1.9"
    value
  else
    :blank_numeric
  end
end

# Error object replacement value.
def ___
  if RUBY_VERSION < "1.9"
    value
  else
    :blank_object
  end
end
```

They are not perfect, but they will help you get through the koans as they were intended.  It's a bad idea to put 'nil' since some tests end up passing if you do.

After we got past that little problem, it became pretty easy to get rolling.  I found that Dennis had the following progression over the course of the hour we worked on this:

* First handful of koans were just getting used to the output and how to interact with the code
* For the next few koans, it was just cut and paste, but without the ability to guess what *should* be in the 'blank'.
* The last section of koans we did, Dennis was able to make educated guesses at what went in the 'blanks' before running the tests.  This was the point that he realized that any mistakes would be pointed out by the tests, but making the guess made him think first.  

And so I think he got to exactly where he needed to.  The koans are a great exercise for coders that are new to Ruby and they are pretty good for new-ish coders too.  They walk you through nearly every aspect of the language.  

I really enjoyed this session since I felt like I learned a bit more how to teach in a pairing session.  Learning to teach is a huge gift in and of itself!  It goes to show you that you can truely learn from pairing with just about anyone, no matter what your respective experience levels are.

On to the next pairing session...
