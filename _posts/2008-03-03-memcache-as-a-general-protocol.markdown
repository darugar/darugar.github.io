---
layout: parand
title:  "MemCache as a General Protocol"
date:   2008-03-03 10:00:00
categories: say/index.php
---
I've been messing around with [Starling](/web/20101222033503/http://rubyforge.org/projects/starling/). Working well so far, although I haven't done anything fancy with it yet.

I also need to create several simple, small, single purpose servers \(eg. one to translate IP addresses to country codes\). I have the python code, I just need to turn them into network accessible servers.

HTTP/JSON would've been my default choice for the service interface. However, taking inspiration from Starling, I'm thinking the memcache protocol is a great general purpose way of exposing services.

The memcache API is simple - get and set - and the data is \(key, value\). The set and get translate well to my interpretation of RESTful GET and POST, and I don't have to worry about the data encoding. There are many memcache client libraries available for many languages, and they've been built with efficiency and speed in mind. Seems like a winner to me.

So all I'd need is a framework for easily putting a memcache interface on a python code base. Know of any?
