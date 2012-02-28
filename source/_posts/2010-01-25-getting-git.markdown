---
layout: post
title: Getting Git
categories: blog
---
I recently converted all of my professional projects over to <a href="http://github.com">github</a> and switched my dev workflow to use git.

Oh, what a difference a tool makes.

First off, git just works.  It's awesome to be able to switch branches *super* easily... and even create a branch after you've begun work on it.  Realizing that you've started a new feature and need it to be in it's own "silo" is great.   What you want is for it not to be a pain to merge it back together.   Honestly, I wish we had this at my old job where having multiple levels and several branches would have been highly beneficial.

Secondly, it is a bit of an adjustment to get your mind around a distributed vcs, but it is very powerful once you're there.  Realizing that a commit is really just versioning off what you have into your local repository and then pushing is really sharing that with some remote repo can be tricky at first.   Once you realize how easy it would be to share and simultaneously work on projects as a result, it is pretty incredible.

To give you an idea, I want to show you a typical svn workflow and the corresponding git workflow.

<code lang="bash">
$ svn co http://svnhub.com/project/trunk
... do some work ...
$ svn up
... resolve some conflicts ..
$ svn status
$ svn commit
</code>

Easy, right?   Yes, it requires very little... but what if you have no network connection?   What if you want to quickly switch a branch?   Nonetheless... lets look at the same kind of thing in git

<code lang="bash">
$ git clone git@github.com:/username/repo
... do some work ...
$ git add <changed files>
$ git commit -a -m "commit message"
$ git pull origin
... resolve conflicts if any ...
$ git push origin master
</code>

So if you're transitioning off of SVN and you want to move to git, that is probably a workflow you will probably become very familiar with--but the power behind it is amazing.  I highly encourage you to watch <a href="http://www.gitcasts.com/posts/railsconf-git-talk">Scot Chacon's 'Getting Git'</a> talk--it will change the way you think about version control!
