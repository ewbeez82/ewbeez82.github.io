---
layout: post
title:  "Re-connecting to an activemq connection"
date:   2014-09-18 09:10:00
categories: java activemq
---

I recently ran across an issue where my application would not re-connect to my ActiveMQ server.  This issue occurred when I needed to take down the activemq server briefly but didn't perform an application restart because there was no need to restart my application.  All of my activemq connections dropped off and never came back!  It's actually suprising that I had never experianced this before.

How to do it? add failover:

{% highlight java %}
failover://tcp://primary:61616
{% endhighlight %}

It's a pretty easy solution and it works well.  It's [documented][failovertransport] on [activmq's][activemq] site.

[failovertransport]:	http://activemq.apache.org/failover-transport-reference.html
[activemq]:		http://activemq.apache.org/

