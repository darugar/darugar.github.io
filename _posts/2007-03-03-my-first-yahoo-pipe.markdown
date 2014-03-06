---
layout: parand
title:  "My First (Yahoo!) Pipe: Fatwallet Deal Watcher"
date:   2007-03-03 10:00:00
categories: say/index.php
---
My laptop broke, leading to a visit to fatwallet, leading to the same old frustration with the lack of a notifier for specific new deals. I decided to finally put together a deal watcher.

I started with the python Universal Feed Reader, which makes it amazingly simple to deal with the fatwallet feed. Part way through I wondered if [Pipes](http://pipes.yahoo.com/) would make my life even easier.

Turns out it does. It's really very easy to put together something as simple as this. All I had to do was fetch the feed and filter it based on my keywords. Two components, 3 minutes, and I'm done. The result is [here](http://pipes.yahoo.com/pipes/ECUqPtTJ2xGqmOHarscPhQ).

It is pretty lame - it doesn't take user input \(I couldn't figure out how to split the user input into multiple words and didn't want to have multiple input fields\). It doesn't have any sort of storage to keep track of what you have and haven't seen. It doesn't actually notify you. It doesn't parse the items to see what the rating is or to filter on it.

However, it is done, and it's now one of my feeds in Google Reader. It'll be interesting to see if it actually meets my needs. Sometimes pretty lame is good enough.
