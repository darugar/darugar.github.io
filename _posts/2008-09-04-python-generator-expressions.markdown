---
layout: parand
title:  "Python Generator Expressions"
date:   2008-09-04 10:00:00
categories: say/index.php
---
I wasn't aware of generator expressions:
    
    
    wwwlog     = open("access-log")
    bytecolumn = (line.rsplit(None, 1)[1] for line in wwwlog)
    bytes      = (int(x) for x in bytecolumn if x != '-')
    print "Total", sum(bytes)
    

Similar to list comprehensions, but evaluated lazily. [Voidspace describes it](http://www.voidspace.org.uk/python/weblog/arch_d7_2008_08_30.shtml#e1008):

> None of the generators are consumed until the final call to `sum`. As it iterates a line at a time \(not keeping the log file in memory\) it can handle huge log files - and as a bonus it runs faster than a typical solution with loops\!

Neat.
