---
layout: parand
title:  "Running Shell Scripts from Python"
date:   2008-05-30 10:00:00
categories: say/index.php
---
There are about a million different ways to execute an external program from Python. Here's the right way:
    
    
    import subprocess
    
    subprocess.call('''zcat %s | tr '\02\03' '\r\n' | ssh %s "hadoop dfs -put - %s"''' %
         (local, DEST, remote), shell=True)
    

Where what you put inside the call statement is what gets executed in a shell. In this case I used pipes, escaping, etc, just to show a slightly complicated example; you could do something as simple as "ls" instead.

Lots more info in [Doug Hellmann's PyMOTW article](/web/20101222040800/http://www.oreillynet.com/onlamp/blog/2007/08/pymotw_subprocess_1.html).
