---
layout: parand
title:  "Map/Reduce (Hadoop) First Impressions"
date:   2008-02-04 10:00:00
categories: stddev
---
I'm finally getting a chance to actually implement map/reduce instead of read or write about it. General impressions so far:

  * Hadoop is fairly easy to install and get running.
  * The choice of Java as the default programming language feels strange to me. It'd feel more natural in Perl, Python, or Ruby since most of what you do is read and massage records. \(I'm actually using Python with Hadoop Streaming\)
  * The map/reduce paradigm is very nice, but doesn't fit everything. In fact, so far it hasn't fit anything I'm trying perfectly. It works, but it always feels like you're shoe-horning the problem into a map/reduce mode. I'm wondering how well it'd work to remove the map/reduce model and make it just a general work distribution mechanism, with map and reduce as easy add-ons. So if I only need a map, or only a reduce, or just a sort, I can do only that. Or, if my map actually produces 2 different sets of output for processing by 2 different sets of reducers, there should be an easy way to do that too.
  * [Pig](/web/20101222053756/http://incubator.apache.org/pig/) is promising; I haven't actually used it hands-on yet. A higher level language seems like the right way to go.
  * Hadoop does scale as advertised, at least to the number of boxes I've tried so far \(30\). It's great to see it crunch through something that used to take 30 minutes in 1 1/2 minutes. I'll be trying larger clusters soon.
