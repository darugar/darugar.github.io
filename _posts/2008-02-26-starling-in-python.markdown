---
layout: parand
title:  "Starling in Python?"
date:   2008-02-26 10:00:00
categories: say/index.php
---
[Starling](/web/20101222053735/https://rubyforge.org/projects/starling/) looks very interesting - it's a "light-weight persistent queue server that speaks the MemCache protocol". To use it you fire up your regular memcached client library, point it at the Starling server, and do a regular _set_ to put an item on the queue, and a _get_ to read an item from the queue. 
    
    
      # Start the Starling server as a daemonized process:
      starling -h 192.168.1.1 -d
    
      # Put messages onto a queue:
      require 'memcache'
      starling = MemCache.new('192.168.1.1:22122')
      starling.set('my_queue', 12345)
    
      # Get messages from the queue:
      require 'memcache'
      starling = MemCache.new('192.168.1.1:22122')
      loop { puts starling.get('my_queue') }
    

This thing is nice in many ways: it's very simple with practically no configuration, ala memcached; it's stable and scalable, running Twitter's production backend clusters; and it speaks a simple and universally available protocol \(memcache\), meaning you can use any of the existing client libraries to access it.

This answers half of my [request for a Python or Ruby messaging server](/web/20101222053735/http://parand.com/say/index.php/2007/09/16/where-are-the-pythonrubyetc-messaging-systems/) \(it does the work-queue half, doesn't do the pub/sub half\). I think I'm going to give it a try. Let me know if you've tried it. 

It also has me thinking - with all of the multitude of async-IO capabilities out there for Python, why isn't there something like this implemented in Python? Between [Twisted](/web/20101222053735/http://twistedmatrix.com/trac/), [asynchat](/web/20101222053735/http://docs.python.org/lib/module-asynchat.html), [Eventlet](/web/20101222053735/http://wiki.secondlife.com/wiki/Eventlet), and the 19 other libraries and toolkits out there, surely somebody smart could whip something together in short order?
