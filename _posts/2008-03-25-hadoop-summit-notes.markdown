---
layout: parand
title:  "Hadoop Summit Notes"
date:   2008-03-25 10:00:00
categories: say/index.php
---
![](http://hadoop.apache.org/images/hadoop-logo.jpg)

Spent the day at the [Hadoop Summit](http://developer.yahoo.com/hadoop/summit/). Here are some notes and impressions, in undetermined order, on 4 hours of sleep:

I was impressed by the level of effort, participation, and momentum behind Hadoop. It's now used in so many places and forms the basis of so many projects I think it has critical mass. Hadoop is poised to be the default implementation of a very important programming model that's about to become a lot more popular.

I was also impressed that several of the talks were on non-Hadoop or not-completely-aligned-with Hadoop technologies - eg. DryadLINQ \(Hadoop alternative\) and JAQL \(Pig alternative\); it was a refreshing change from the vendor-pitch conferences and talks I've seen lately.

Random notes:

**[DryadLINQ](http://research.microsoft.com/research/sv/DryadLINQ/)** - treats the data flow as a general graph instead of forcing it into map/reduce. That seems quite nice, although someone did point out map/reduce generalizes to any graph, so it's only a matter of efficiency. Would be interesting to find out how much efficiency and/or more natural programming paradigm there is in Dryad. Apparently it'll be open sourced at some point in time.

DryadLINQ integrates with [LINQ](http://en.wikipedia.org/wiki/Language_Integrated_Query); in effect Dryad becomes an implementation provider for LINQ. This is also very attractive - to use DryadLINQ you simply write regular LINQ, no special language to learn. I've heard nothing but good things about LINQ, so this seems good. As Micheal pointed out there are a number of other implementation providers for LINQ, such PLINQ for parallelized LINQ on multi-core processors, that DryadLINQ can take advantage of for free. 

LINQ is also nicely integrated with .Net, meaning it's available in a number of languages including C\#, so you have access to the full language alongside Dryad. You could write regular C\# + LINQ code, flip a switch, and have it run on the grid.

**[Zoo Keeper](http://zookeeper.sourceforge.net/)**. Now this one was interesting - an approach to distributed coordination with simple semantics and good performance. It works something like this: Zoo Keeper provides atomic reads and writes on "nodes", which are simply pieces of data with a name. It uses a filesystem-like setup, so you create nodes in a directory structure - eg. you can write to the node "/servers/slaves/slave-23″, and others can read from it. Processes can set "watch"es on nodes, allowing them to be notified when the node is changed. 

![ZooKeeper](http://zookeeper.sourceforge.net/Figures/service.png)

High performance is achieved by containing the data in memory. Reads can be serviced by any ZooKeeper server and writes are handled by the "leader".

There's a lot more to Zoo Keeper, check out their site to see more. I'm hoping someone will use it to build a simple queue + pub/sub server.

The [X-Trace](http://x-trace.net/wiki/doku.php) talk was also quite good. In short they patched Hadoop to throw X-Trace events, allowing them to instrument and visualize full execution path of map/reduce jobs. They had a couple of interesting examples - improving processing time of the full Wikipedia corpus from 2 hours to 8 minutes by realizing the reduce step was only running on 2 boxes, and finding a faulty/flaky disk by looking at graphs of the performance of a lagging server. 

X-Trace integration is due to be submitted for inclusion into the Hadoop source. I'm thinking some of the visualization graphs they showed \(particularly the toothbrush looking one showing machine utilization for map and reduce steps\) should be part of core Hadoop, available for every map/reduce run for free. It's pretty coarse grain info \(which machine was running what when\), so it can probably be divined from info Hadoop already spits out without the X-Trace additions.

**HIVE** was very interesting. FaceBook's internal data warehouse infrastructure, implemented as a query language on top of Hadoop. They found people are looking for two ways to access the warehouse: the analysts want SQL-like interfaces, and the programmers want to program in any language they want. The former is available via a query language they invented, and the latter is implemented by Hadoop Streaming. 

Hive is in use by ~40 people or ~25% of FaceBook's engineering team \(thus FaceBook's engineering team size is 40\*4 = 160\). It stores a total of 22TB of compressed data, with ~200G daily increase.

There was a lot more to the summit; maybe I'll write up the rest later. 

Final thought: you could really see the power of open-source at play here. With so many people not only using Hadoop but also taking so many different approaches to building systems on top of it \(Pig, JAQL, Hive, Cascading, HBase, Mahout, X-Trace, the Amazon-EC2 integration\), you have to think it's going to become the most vibrant implementation of Map/Reduce out there.
