---
layout: post
title: "Pairing Post Mortem - @javichitone - Improving a Gem"
date: 2013-05-22 23:15
comments: true
categories: blog pairing post-mortem ruby
---

I had my first international pairing session with [@javichitone](http://twitter.com/javichitone) tonight.  He's from Peru and will soon be graduating.  He should have no trouble finding a job based on the code I got to read of his :)

We talked for a bit and settled into looking at a gem he recently published.  Since it was his gem, I elected to drive.  I'm familiar enough with gems that I'm comfortable in *general*, but he knew the *specifics* of his gem, so to get the most out of it, he needed to be commenting on the specifics he knew and I needed to be diving into figuring out those specifics.

We got his tests running very quickly since he had the gem set up perfectly.  A clone and a quick <code>bundle install</code> and we were ready to <code>rake test</code>.  I'd never used MiniTest, but it seemed simple enough to switch to after knowing RSpec.  All the tests passed, so we were in a position to add features or improve the code.

We did a little of both.  The first thing we did was improve performance.  One observation about improving performance: there are often no tests to write... you just make sure, functionally, that you're still passing and then set up a benchmark or direct observation that you're seeing improved performance results.  It wasn't hard to do a quick cache of the HTTP requests to speed things up significantly. Javier was surprised that you could use an array as key to a hash, but grasped very quickly the "trick" after seeing it.

After that, we decided to improve the API.  Javier's [Lyricfy](https://github.com/javichito/Lyricfy) gem lets you easily search a few sites for lyrics of popular songs.  The gem scrapes the lyrics off of certain sites and put the lines of lyrics into an array.  I wanted to be able to type <code>puts song.body</code> rather than <code>song.body.each {|line| puts line}</code> so we did something sneaky and defined a singleton <code>to_s</code> method on the <code>song.body</code> array and that's all we needed.

I have *never* in 5 years of being a Ruby programmer found reason to redefine <code>to_s</code> on an instance of an Array, but tonight it seemed like the perfect use of such a thing.  I love how pairing gives me new opportunities to use things I've learned, but remained dormant because I don't ever look at things in a way that lets me use them.

We submitted two pull requests to his [gem](https://github.com/javichito/Lyricfy) and called it a night.  I'm looking forward to another session with Javier.  

On to the next pairing session... 
