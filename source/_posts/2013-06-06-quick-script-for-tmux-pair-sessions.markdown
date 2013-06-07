---
layout: post
title: "Quick Script for TMUX pair sessions"
date: 2013-06-06 09:33
comments: true
categories: pairing code shell tmux blog
---

I wanted a quick and easy way to set up a new TMUX session with a brand new pair, so I came up with this:

``` sh ~/bin/pair-session
#!/bin/sh
gh-auth add $1
sudo cp ~/.ssh/authorized_keys /Users/pair/.ssh/authorized_keys
sudo chown pair:staff /Users/pair/.ssh/authorized_keys
gh-auth remove $1
tmux -S /tmp/pairing new -ds pairing && chgrp staff /tmp/pairing && tmux -S /tmp/pairing attach -t pairing
sudo rm -f /Users/pair/.ssh/authorized_keys
```
That will download ssh keys, create a tmux session, and attach to it.  When you're done it will cleanup so the other person has no access to your box.

And I have a <code>pair-session</code> script in the <code>/Users/pair/bin</code> directory that looks like this:

``` sh /Users/pair/bin/pair-session
#!/bin/sh
tmux -S /tmp/pairing attach -t pairing
```

## Usage

You can invoke the host one like this: <code>pair-session marksim</code> (replacing <code>marksim</code> with whatever github user you want to pair with)

And your pair simply has to type <code>pair-session</code> to connect.


## Requirements

* [github-auth](https://github.com/chrishunt/github-auth) gem (which requires Ruby 1.9)
* ability to sudo 
* a user called 'pair' that has SSH (a.k.a. [Remote-Login](https://raw.github.com/chrishunt/github-auth/master/img/mac-os-ssh-sharing.jpg) on OS X) enabled
* an editor that works in the terminal :)

## Positives

* The user does not have access to your files since they're not SSHing in as you
* No need to install a system wide RVM or Ruby 1.9 for github-auth -- this copies the <code>.ssh/authorized_keys</code> into your pair account
* Besides creating a user, **you can have a TMUX-ready pair session with a brand new pair ready in under 10 seconds.**
* Automatically de-authorized the user once you're done.

## Negatives

* I wish it didn't have to copy <code>authorized_keys</code> -- maybe it's worth hacking to not require <code>github-auth</code>?
* It requires a sudo password -- and can require it twice if your session goes on long enough.
* Currently, specific to OS X (/Users/, and the 'staff' group)

Anyway, I hope it's useful to others as a simple way to set up your box for pairing.

