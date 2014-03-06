---
layout: parand
title:  "The Hamburger Theory of Threads and Processes"
date:   2008-06-03 10:00:00
categories: stddev
---
![Hamburger](/web/20101222043127im_/http://farm4.static.flickr.com/3103/2516409131_a7770858bf_m_d.jpg)

You're busy making hamburgers and suddenly you get lots of customers. You want to scale your service to take care of more customers more quickly.

Threads: all of your workers share a single set of tools, utensils, and the same workspace. One puts mustard on the spreader, turns to grab the bun, and finds that someone else has put ketchup on there while he was turning. So you come up with complex rules about who must ask permission, under what circumstances, for grabbing what tools. Sometimes worker A is waiting for worker B to put down the knife, while B waits for A to put down the cheese, and they end up waiting forever.

Processes: each worker gets his own tools, utensils, and work space. Any sharing is explicit: worker A must intentionally pass the utensil to worker B.

More tools are used with processes, so in some sense it's less efficient. But the rules are much simpler.

If the tools and utensils are very large and valuable, perhaps threads will work. Picture lots of bees each working on a piece of the beehive.

When the tools are small their duplication is less wasteful. The simplicity of the rules makes it easy for you to get your system going, add new items to the menu, and spend a lot less time worrying about your workers waiting for somebody else to put down the cheese.

Photo by [JustABigGeek](/web/20101222043127/http://flickr.com/photos/justabiggeek/).
