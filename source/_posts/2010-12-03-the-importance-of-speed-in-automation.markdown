---
layout: post
title: The Importance Of Speed in Automation
categories: blog
---
We are impatient people.  This is something that we must work to fix in order to grow as individuals, but it is something that serves the automator well--or can be our downfall.

Joel Splosky wrote on the "<a href="http://www.joelonsoftware.com/articles/fog0000000043.html">Joel Test</a>" that having anything less than the best tools money can buy is rediculous for a development team.  The reasoning is this:  If you're paying developers what they are worth, then they are expensive, and wasting their time while they're reading the Onion waiting for a build will kill your productivity--and your bottom line.

The same goes now for Test Driven Development.  Having a great test suite is nearly essential, and anything more than a trivial application will have difficult and long running tests, but these tests must be managed well and there must be a way for a developer to quickly run through a cross section of the test suite as a sanity check before checking in.  If your tests take 1 minute to run, then the developer is 6 times less likely to run them than if they take 10 seconds to run.  If your tests take 30 minutes to run, then the developer is 60 times less likely to run them than if they take 30 seconds.  Every additional test is great for coverage, but if it adds time, there is a point of diminishing returns.

Tagged tests are a must, and a solid set of fast tests that touch much of the code base is essential.  It must also be easy to run individual tests--anything that hampers this reduces the liklihood of continued test driven development.  Testing becomes a chore again and running the tests becomes an <a href="http://xkcd.com/303/">excuse for swordfighting</a> in the hall.

So take the time to improve the speed of anything you wait on as developers--and reap the benefits tenfold. 
