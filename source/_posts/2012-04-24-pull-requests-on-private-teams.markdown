---
layout: post
title: "Pull Requests on Private Teams"
date: 2012-04-24 16:17
comments: true
categories: blog, meta, git
---


Pull Requests are used often in the open source world, but less so on private teams.  They are a great way to provide an automatic, team-wide code review mechanism.  If your private team doesn't use pull requests, I'd encourage you to investiage it.

Why would you move your team over to pull requests?
---------------------------------------------------

* it provides a mechanism for code and source control review
* it gives more visibility and accountability to the whole team
* you can (optionally) restrict access so only trusted members bless the merge


What is the Pull Request process like?
----------------------------------------------------

There are lots of resources about [how to submit pull requests](http://railscasts.com/episodes/300-contributing-to-open-source?view=asciicast) out there, but the basics go like this.

1. If you want to restrict access, have developers fork your repository from github.  Otherwise, you can simply submit pull requests from feature branches.
2. From the release branch, the developer creates a feature branch, does work, and pushes it to their fork
3. From github, the developer can click the "pull request" button on that branch, github even has a "recently pushed branches" section now!
4. From there the developer can review the pull request commits and diff to confirm conciseness and clarity.  
5. After submission, anyone with read access to the main repository can review and comment on the pull request (including inline comments)


What makes a good pull request?
-------------------------------

This is a much harder question to answer, since it is, in fact, subjective.  However, I do think there are some good guidelines nearly any team could follow.

A Good Pull Request is...

* <strong>Concise</strong> - Less than 200 changed lines.  Preferably less than 50.  If you need more to solve your problem, break your problem into smaller pieces.
* <strong>Clean</strong> - It follows the "single responsibility principle" in the fact that it's only solving one problem.
* <strong>Related to a Ticket</strong> - Since it's only solving one problem, that problem should be documented in a ticket in whatever bug tracking system you have.  
* <strong>Tested</strong> - Some kind of automated test should be included within all but the most trival pull requests.  This provides increasing coverage and tests to document and prove the problem is fixed.

Pull Requests have changed the way our team does work.  If you are on a private team and arent' using them, I'd highly recommend trying it out on one of your projects.

