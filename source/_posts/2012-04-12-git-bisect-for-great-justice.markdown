---
layout: post
title: "Git Bisect For Great Justice"
date: 2012-04-12 11:29
comments: true
categories: blog git code shell
---

About a week ago, we had an elusive error that appeared when we deployed our latest app to staging.  Suddenly, any submission resulted in a "Stack trace too deep" error that gave no meaningful way to determine where the issue was coming from.  We were stuck for a couple of days, but then I was reminded of <code>git bisect</code>.

<code>git bisect</code> is a great way to trace down problems to a specific commit for purposes of isolation or blame (though I'd suggest against the latter).  Like you'd expect from a programmer, it even searches efficiently, using a binary search, hence bisect.

Fundamentally, what <code>bisect</code> does is split the commits from the latest good commit to the earliest bad commit in half over and over again until one commit has been isolated which transition occurred.

Let's say that you were a terrible developer and didn't run your tests before checking in.  After several days of doing this, you run your spec suite and get an unhelpful error which prevents the spec suite from even being run.  Since you don't know when that was introduced, you use <code>git bisect</code>

``` bash 
$ git bisect start
$ git bisect bad # marks the current commit as bad
$ git bisect good production #marks the commit pointed to by 'production' (branch or tag) as good
Bisecting: 62 revisions left to test after this (roughly 6 steps)
``` 

Now you are in the middle of bisecting.  You can then attempt to run specs (or manually test for an error) and mark the commit accordingly

``` bash
[3939bac050b2779d5d13a3757054511eb0f8961a] Update Rakefile to point to sensible server.
$ rake spec
ERROR! ...
$ git bisect bad
Bisecting: 31 revisions left to test after this (roughly 5 steps)
[f2230b2e2ccf636266891ce6be3750994f414fe4] Fixing Issue #2294
$ rake spec
.......  ^C
$ git bisect good
...
```

You continue until you've isolated the commit...

``` bash
$ git bisect good
1c675b26e5b8472d28d3fb44a23119ba41e7002c is the first bad commit
commit 1c675b26e5b8472d28d3fb44a23119ba41e7002c
Date:   Wed Apr 4 16:11:40 2012 -0500

    Adding support for Guard
```

Then you can look at that commit and address it specifically.  This is a huge argument for small commits, especially when you're looking for small, difficult to find bugs related to subtle business logic.

When you're done, just <code>git bisect reset</code> and you'll be back on your <code>HEAD</code>.  

You may be asking if you could do this manually -- and then answer is an absolute YES, but <code>bisect</code> provides a very simple and easy way to step through the process without a lot of extra thought or effort.
