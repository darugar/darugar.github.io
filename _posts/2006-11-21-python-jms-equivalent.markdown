---
layout: parand
title:  "Python JMS Equivalent?"
date:   2006-11-21 10:00:00
categories: stddev
---
I'm thinking through an implementation that I'd like to scale some day. Essentially it's a message processing system with a small bit of state to pass around. Mostly it's a matter of handing messages off between various workers.

In Java world I'd do this with threads. If I wanted to think across boxes I'd throw in some sort of persistent queue, likely JMS.

But I'm in the Python world. I could do threads \(btw, how well do threads work in Python in both windows and linux?\), but I'm on a non-threads kick at the moment and would like to go the multi-process/message passing route.

What I'm looking for is a JMS equivalent for Python - a persistent, reliable message passing system with a clean API that can be used on a single machine/single processor system just as well as on a multi-machine/multi-processor network of systems.

I looked briefly - I could do something with [xmpp](/web/20101222035826/http://www.xmpp.org/), there's [spread](/web/20101222035826/http://www.spread.org/), or I could put the queue in a database. But none of them are satisfactory.

How are people doing persistent queues in Python? Is there a JMS like device?
