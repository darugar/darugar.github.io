---
layout: parand
title:  "Python Script For Finding And Removing Duplicate Files"
date:   2008-10-15 10:00:00
categories: say/index.php
---
My image, mp3, and ebook collection were a mess after years of copying to various servers, consolidating, and re-copying. I had lots of duplicates.

I looked for an app to find and remove duplicates but surprisingly didn't find anything very good. So I had to write my own.

This is a very simple script - it scans the directory tree you specify, looks for exact duplicates, and removes the duplicates.

It's not very smart about which copy it removes. It's not smart about finding files that are "similar" - it only finds exact matches. It ignores small files \(intentionally - it's easy to make it deal with small files\).

It uses /temp for its output and cache files, so it's targeting windows. Change that to /tmp if you're running unix.

I built in a caching mechanism to save the results of scanning the disk, but it turned out not to be too useful and the script ran faster than I expected, so the caching is commented out.

Here it is: [FileInfo.py](http://parand.com/say/misc/FileInfo.py) .
