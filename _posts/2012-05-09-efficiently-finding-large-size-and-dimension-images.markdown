---
layout: parand
title:  "Efficiently finding large (size and dimension) images"
date:   2012-05-09 10:00:00
categories: stddev
---
I needed to efficiently find large images \(those with dimensions greater than x\). Here's what I came up with:

First, find images whose file size is greater than 3M:
    
    
    find . -name '*jpg' -size 3M > /tmp/big-receipts.txt

Now, get the dimensions of each of those images using imagemagick's identify command line utility. The key to using this thing efficiently is to include the "-ping" flag \(believe it or not that took me quite a while to figure out\):
    
    
    identify -ping filename.jpg

displays this type of output:
    
    
    /tmp/big.jpg JPEG 10200x13200 10200x13200+0+0 8-bit DirectClass 5.54MB 0.000u 0:00.000

Now we can put the two together:
    
    
    for fname in `cat /tmp/big-receipts.txt`; do identify -ping $fname; done
