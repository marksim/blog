---
layout: post
title: "Pairing Post Mortem - @jnanney - OAuth"
date: 2013-07-18 11:34
comments: true
categories: blog pairing post-mortem ruby vim
---

I finally got a chance to pair with [@jnanney](http://twitter.com/jnanney) tonight.  He had a project dealing with the OnStar API that needed OAuth Authentication, so we took a stab at implementing it.

## Setup

* Skype - TIL Skype 6.x turns off your video if you connect to a Skype 2.0 client--but the audio still works!
* TMUX+VIM on a slice (not local) 

## Experience

We started by making some large, rough ideas about what we wanted to accomplish and then began looking up some things on OAuth2 to help us accomplish them.  Pretty quickly we stopped driving everything via tests and started exploring via <code>IRB</code>.

We struggled quite a bit with the OnStar OAuth2 documentation... figuring out what the endpoint was.  We also needed to know how to get a token from the command line.  We spent most of our time just digging around in the documentation and IRB. Eventually we disovered what we wanted to call and headed that direction.  By that time, it was time to wrap up our time.  

## Takeaways

* On Ubuntu, <code>vi</code> isn't compiled with ruby support, but <code>vim</code> is.  Weird.
* In VIM, <code>dt<character></code> will delete everything from the current marker to the character you specify
* Documentation matters a lot
* Just moving a little bit down the road is often enough.  Even though we didn't make more than about 20 lines worth of progress (including tests), we moved far enough that he was able to finish out the feature by the next day.

It was great pairing with Jim.  Looking forward to it again in a few weeks.

On to the next pairing session...
