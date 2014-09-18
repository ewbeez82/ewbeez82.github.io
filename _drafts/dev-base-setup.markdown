---
layout: post
title:  "Base setup for software development"
date:   2014-09-18 09:10:00
categories: development blog software java devops microservices docker
---

In this post, I will discuss what it takes for a software development base setup. None of this is new, it's all been discussed over and over again on the net but it helps to have a good refresh every now and again.

Prehistoric Basics
------------------
This is the stuff that, if your doing software development in the last 10 years you should definatly be doing.

Version Control
===============

Version control systems have come a long way over the years.  At this point, I would say it makes sense to use git in most cases.  Especially for a new development effort.  Git is a proven system and it's widely adopted.  Older systems such as svn can be used but these days, for me it simply makes sense to use git.

If you or your team isn't using version control you need to be.  It's really as simple as that.  There is no good reason to not use version control and it's extremely risky not to use version control.  Do I really need to go beyond that?

Build System
============

Version control is great but it's really just the starting point.  Continuous integration systems have been around for a long time as well.  Once you checkin something to version control the CI server is going to build it as a first step.

Test 
====

As part of the automated build, a number of automated tests can be kicked off as a trigger from a successful build.

Once these are established you can move into devops.

Devops
------

While not necessarily devops specifically you do need to be able to do the following.

Deployment System
=================

Deployments, ideally should be a push button event.  This is possbile with a system like Go. Go allows you to setup pipelines including manual processes.  Each build can to to a point where it's ready for deployment.  Deployment to production should often be a manual decision but it should not be a manual process.

Monitoring
==========

Once your system's live, it should be monitored.  System monitoring is a huge topic and there is a lot of ways to do it.

Fallback
========

As your environment get's more advanced you can have automated systems for performing a failback/rollback.  This follows the circuit breaker methodology.

Microservices
-------------

Finally, you can get to microservices!!! They are conceptually an easy idea.  A simple service with a single responsibity.  Isolated and statelesss.  Sounds awesome! And they are pretty easy to write, but how do you manage it all?  Well to start with you have to have an inferastruture that, at a minimum, supports everything above!

* Security
* Monitoring
* Service Discovery
* System Fallback / failover
* Api-Gateways

It occurred to me a while back that a microservices architecuture likens it's self to what an application server does but it's distributed across the network as well as small services.

Other
-----

There is a number of other practices that you should adopt as well such as having a postmordum, asking the 5 why's to never let the same problem bite you more than one time.


