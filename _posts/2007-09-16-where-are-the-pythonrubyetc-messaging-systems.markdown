---
layout: parand
title:  "Where Are the Python/Ruby/etc Messaging Systems?"
date:   2007-09-16 10:00:00
categories: stddev
---
Scaling requires the ability to decompose apps into pieces which can be spread across multiple boxes. An application composed of multiple pieces needs an efficient, reliable way to communicate between the pieces. 

With multiple cores now standard, even in a single box scenario we need pieces that can run independently and communicate efficiently. 

Java has this via JMS, with multiple good implementations, both open and closed source.

So where are the high quality, standard communication pipes for scripting languages? Where is the equivalent of JMS for Python?

I realize I can use [ActiveMQ](/web/20101222051640/http://activemq.apache.org/) with [HJB](/web/20101222051640/http://hjb.berlios.de/) and [PyHJB](/web/20101222051640/http://cheeseshop.python.org/pypi/pyhjb), but I'm loathe to introduce three pieces of new software along with a new VM \(the JVM required to run ActiveMQ\) into the picture. 

What I'm looking for is a standard interface for messaging that allows implementations that optimize both intra and inter box scenarios. It should allow work-queue scenarios as well as pub/sub. It should support persistence / fail-safe modes. It should enable message or event driven apps - ie. have a event loop that's driven by message availability, ala MDBs in the Java world.

Is there such a thing and I've missed it? Or is it that no-one wants it? 

I suppose there's always [Gearman and TheSchwartz](/web/20101222051640/http://www.danga.com/gearman/)…
