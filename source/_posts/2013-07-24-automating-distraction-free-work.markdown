---
layout: post
title: "Automating Distraction-free Work"
date: 2013-07-24 12:16
comments: true
categories: blog productivity
---

I've followed the [Pomodoro Technique](http://www.pomodorotechnique.com/) for a few years now.  I've tried several different tools to get it where I want, but in the last few months I've begun using *AppleScript* to automate things that I want done in my environment every time I start/finish a Pomodoro.

I use [Things](http://culturedcode.com/things/) as well to keep track of my tasks.  I think GTD and the Pomodoro Technique are a wonderful marriage where GTD gets to keep track of the What and the Pomodoro Technique motivates to to actually make progress.  It's all too easy to [feel like you're making progress](http://timemanagementninja.com/2012/01/8-reasons-you-arent-getting-things-done/) by simply moving tasks around and "getting organized."

So when I combined these two techniques, I used [Pomodoro.app](https://github.com/ugol/pomodoro) -- which is no longer available on the App Store, but you can easily download it and compile it with XCode. 

I have 4 scripts that I use for managing the link:

``` applescript Start
tell application "System Events" to if exists process "Things" then
  tell application "Things"
    set pomoName to "$pomodoroName"
    set createToDo to true
    repeat with todayToDo in to dos of list "Today"
      set toDoName to name of todayToDo
      if toDoName starts with pomoName then
        set createToDo to false
      end if
    end repeat
    
    if createToDo is true then
      set newToDo to make new to do with properties {name:pomoName} at end of list "Today"
    end if
  end tell
end if

do shell script "cp /etc/hosts ~/.old-hosts; sudo echo '127.0.0.1 facebook.com www.facebook.com netflix.com movies.netflix.com twitter.com youtube.com www.youtube.com' >> /etc/hosts; dscacheutil -flushcache" with administrator privileges
```

This script finds a TODO with the appropriate name and creates it.  Pomodoro.app tries to do this, but it doesn't work when you add [X] to the title to indicate the number of pomos. 

It also blocks facebook, netflix, twitter, and youtube so you can reduce your distractions automatically during your pomo.

``` applescript Interrupt
tell application "System Events" to if exists process "Things" then
  tell application "Things"
    repeat with possibleToDo in to dos of list "Today"
      if name of possibleToDo starts with "$pomodoroName" then
        set currentName to name of possibleToDo
        set name of possibleToDo to currentName & " [']"
      end if
    end repeat
  end tell
end if
```
During an interruption, this marks a small <code>[']</code> on your task.  This lets you see which kinds of tasks get you interrupted the easiest when looking over your day.

``` applescript Reset
do shell script "sudo mv ~/.old-hosts /etc/hosts; dscacheutil -flushcache" with administrator privileges
```
When you reset your pomo, this unblocks all the websites that you originally blocked.

``` applescript End
tell application "System Events" to if exists process "Things" then
  tell application "Things"
    repeat with possibleToDo in to dos of list "Today"
      if name of possibleToDo starts with "$pomodoroName" then
        set currentName to name of possibleToDo
        set name of possibleToDo to currentName & " [X]"
      end if
    end repeat
  end tell
end if

do shell script "sudo mv ~/.old-hosts /etc/hosts; dscacheutil -flushcache" with administrator privileges
```
After a successful pomodoro, this script finds the task you were working on in Things and adds a <code>[X]</code> to the end of the title so you can see how many pomos you actually spent on it.

It also unblocks the blocked websites.

All this together makes for easy to prep, easy to review, and relatively distraction-free work.  
