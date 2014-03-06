---
layout: parand
title:  "Python Scripts For Dumping Oracle Data And Loading Onto Hadoop DFS"
date:   2008-10-22 10:00:00
categories: say/index.php
---
There have been several requests for this, so I might as well post it here for general use. I put together a simple system for dumping data out of Oracle databases and loading onto Hadoop DFS. The slightly interesting part is the parallelism - [Python's Processing library](http://pyprocessing.berlios.de/) is used to dump partitions in parallel and copy and load them onto DFS in parallel. This helps when dumping large amounts of data from partitioned Oracle tables.

The database interaction is handled by [db.py](http://parand.com/say/misc/db.py) . There are a couple of helper functions for finding table partitions, etc. DBDumper dumps the requested fields from the requested table:
    
    
    dumper = db.DBDumper('username/password@yourhost:9999/DB', 'table_name',
          ('field1', 'field2', 'field3'), 'owner', 'partition', 'output_dir', 10)
    dumper.dump(cp)
    
    

Where 10 is the level of concurrency, _owner_ is the owner of the table, and _partition_ is the name of the partitions you're interested in \(can be None\).

[dfs.py](http://parand.com/say/misc/dfs.py) copies the dumped files over in parallel, again using PyProcessing. It's simply a wrapper around "cat | ssh | hadoop dfs -put". 

DBDumper and dfs are tied together via a callback - when each partition is dumped, the callback is invoked, triggering the dfs copy. 

Here's a complete example of using these to dump and copy data:
    
    
    import db
    import dfs
    
    fs = dfs.RemoteDFS('address.of.remote.machine')
    
    def cp(arg):
        print "CALLBACK:", arg
        fs.cp(arg[0], '/some/directory/' + arg[1] + '/' + arg[2])
    
    dumper = db.DBDumper('username/password@yourhost:9999/DB', 'table_name',
         ('field1', 'field2', 'field3'), 'owner', 'partition', 'output_dir', 10)
    dumper.dump(cp)
    
