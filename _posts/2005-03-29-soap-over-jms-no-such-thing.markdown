---
layout: parand
title:  "SOAP over JMS: No Such Thing"
date:   2005-03-29 10:00:00
categories: say/index.php
---
[Subbu Allamaraju](http://www.subbu.org/weblogs/welcome/2005/03/soap_over_jms.html) makes an excellent point: there is no such thing as SOAP over JMS. It simply doesn't make sense.

JMS is a set of APIs. It is not a transport or a protocol. You can implement JMS on any kind of transport; I could use messenger pigeons or smoke signals as the transport for a JMS system. 

So let's stop saying SOAP over JMS. It's very misleading - the majority of people, particularly those a vendor has spoken to, assume it's possible to have something that listens to any JMS system and picks messages off the wire. I've heard smart people ask for "a generic monitoring system for SOAP messages over JMS". There's no standard wire, so you really can't do that. 

JMS specifies the two ends \(publishing and subscribing APIs\), but not the middle. A transport specifies the middle. That's what you need to send SOAP over.
