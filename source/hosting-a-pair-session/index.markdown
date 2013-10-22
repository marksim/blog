---
layout: page
title: "Hosting a Pair Session on Mac OS X"
date: 2013-08-07 09:06
comments: true
sharing: true
footer: true
---

There are basically 2 options for hosting a pair session, one is Screen Sharing, which is straightforward and easy to do.  Check out [ScreenHero](http://screenhero.com) or [TeamViewer](http://teamviewer.com) if you're interested in that.  At this point in time, ScreenHero is free, but almost all of these services are expected to eventually charge.  Your experience may be less than optimal due to bandwidth/networking issues.  Some people have no problems, some struggle.

That's why it's really valuable to be able to host on your own box, with all it's developery power at no additional cost.

I'm going to walk you through the steps of how I do it.  There may be many other ways, but this is simple, secure, and once you've done the initial setup, it's very easy to pair with someone new.

### Initial Setup

You will only have to perform these steps once per machine that you want to pair on.

1. Set up a standard user on OS X by opening the System Prefs and going to "Users and Groups".  From there, unlock the pane and add a new user named "pair".

    {% img /images/user_setup.png 500 %}
 
2. Go to the Sharing pref pane and enable Remote Login - make sure that if you only enable it for certain users, that your "pair" user is in there. 

    {% img /images/remote_login_setup.png 500 %}

3. Finally, open up a terminal and type the following
```
    $ sudo su pair
    $ cd 
    $ mkdir .ssh
    $ echo "tmux -S /tmp/pairing attach -t pairing" >> ~/.bash_profile
    $ echo "exit" >> ~/.bash_profile
    $ exit
```
4. Download this [pair-session](https://gist.github.com/marksim/5785406/raw/c986c8882661a47d422d899d89c3fe44c7979f96/pair-session.sh) script.
5. Find the script and copy it into your path.  I put mine in `~/bin` and add that to my path in my `~/.zshrc` file.  Make sure you `chmod 755 ~/bin/pair-session.sh`

### Research

In order to host this on most home networks, you'll need to port forward from your router to the IP of your development machine.

To do this, you need two things.

1. **Find your local IP.**  `ifconfig` will show it under `en0` or sometimes `en1`.  You can also try `ipconfig getifaddr en0` which should return it on most standard Macs. 
2. [Look up your router](http://portforward.com/english/routers/port_forwarding/routerindex.htm) and follow the instructions for setting up port forwarding to that IP.  **You will want to forward port 22**.

You *probably* want to turn this on and off between each session since it's less secure and your local IP may change.  If you can find a way to automate it, there are places in the script that you can include punching and patching the port. 

### Each Session

You are now completely setup and ready to go.  In order to start a session, ask your pair what their github user name is and type:

    $ pair-session.sh <username>

The ssh command needed for your pair is already copied onto your clipboard.  Just hit `CMD-V` in the chat window to let your pair know how to connect.  

As soon as they ssh into your box, you will both be able to control the same cursor on the TMUX session you are in.

### That's it!

The initial setup takes about 15-30 minutes depending on your level of comfort.  After that, you will be able to setup a pairing session with anyone who has a github account in less than 10 seconds.  

Happy Pairing!

