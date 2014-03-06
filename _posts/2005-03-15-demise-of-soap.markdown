---
layout: parand
title:  "The Demise of SOAP"
date:   2005-03-15 10:00:00
categories: say/index.php
---
"What do you think about the whole SOAP vs. REST thing?". I hate this question, but it comes up all the time. Who cares? It's all just XML over HTTP\*. I don't care about SOAP vs. REST. 

My traditional answer has been: REST is great for simpler projects where the verb vocabulary fits the limited HTTP set, but as you look to add capabilities, you'll invariably invent an envelope, and then some way of describing your service, so why not use SOAP and WSDL.

But this is not working. I've been publicly advocating SOAP for a long time; in fact, in a past life I started a company in that space. So it's not easy for me to say this, but SOAP is in deep trouble. And when I say SOAP, I mean the whole SOAP+WSDL+UDDI+WS-\* bundle, since the term Web services is ambiguous and includes REST for some people.

**The problem is [our obsession with constantly inventing new specifications](http://www.tbray.org/ongoing/When/200x/2005/03/12/WSDM-Disapproval) instead of pausing and fixing the existing ones based on real world feedback.**

To all you WS-\* inventors out there: [Look](http://norman.walsh.name/2005/02/24/wsdl). Look people, [look](http://www.redmonk.com/jgovernor/archives/000474.html), [look](http://www.tbray.org/ongoing/When/200x/2005/03/11/WSInTheSpring), [look](http://developer.yahoo.net/faq/#soap), [look](http://www.artima.com/weblogs/viewpost.jsp?thread=95113). Very smart people are having a lot of trouble with SOAP. Do you not see this as a problem? Do you see any of these problems being fixed by your new specification? Or should we pause for a minute, **get the basics right, grow the whole market**, and then address the higher level issues?

Let me point out the obvious: the whole Web has been built on simple little HTTP. How about that HTTP-DistributedManagement spec? How about that one about routing it through all kinds of actors and intermediaries? You hadn't heard of those? It's because they don't exist.

This feels like dejva-vu; I [wrote about this in 2002](http://www.newarchitectmag.com/documents/s=7221/na0702j/index.html), and likely will again in the future. But let this be another data point: a hard-core, first-in-line SOAP guy is getting seriously turned off by this whole mess. REST is looking more attractive every day. 

\* Yes, I know SOAP is over "any" transport, but pragmatically speaking.
