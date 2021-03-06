---
layout: parand
title:  "D Lazy Evaluation Prettyness"
date:   2008-06-27 10:00:00
categories: say/index.php
---
[This](http://www.digitalmars.com/d/2.0/lazy-evaluation.html) is kind of pretty:
    
    
    void log(lazy char[] dg)
    {
        if (logging)
    	fwritefln(logfile, dg());
    }
    
    void foo(int i)
    {
        log("Entering foo() with i set to " ~ toString(i));
    }
    

Note the **lazy** keyword in the definition of the log function, which tells D to only evaluate the value if needed \(ie. lazily\).

Nice. Smells a little like [Twisted's deferred business](http://twistedmatrix.com/projects/core/documentation/howto/defer.html), except different.

Via [Raganwald](http://weblog.raganwald.com/).
