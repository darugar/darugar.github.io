---
layout: parand
title:  "The Performance Penalty of Virtualization"
date:   2008-06-27 10:00:00
categories: stddev
---
If you've spent any time with virtualized environments you know how effective and productive they are. The process of expanding capacity for [FaceDouble](/web/20101222043115/http://faceddouble.com/), for example, became significantly simpler once they moved to depolying virtual servers, and SmugMug has been [singing the praises of Amazon's EC2](/web/20101222043115/http://blogs.smugmug.com/don/2008/06/03/skynet-lives-aka-ec2-smugmug/) with a clever system to provision and remove capacity based on load. My own experiments with [Hadoop](/web/20101222043115/http://hadoop.apache.org/core/) and EC2 have been similarly fruitful.

So I'm wondering what the downside to aggressively going virtual is - why not make all servers virtual?

The main issue that comes to mind is performance, or the loss thereof. Presumably the performance of a virtual server is less than that of the same server running directly on the native OS.

Just how much of a performance difference is there, say in terms of per request latency and capacity, for a web server, a database server, and a cpu-bound heavy computation server, for any of the common virtualization systems \(Xen, VMWare, etc\)? I haven't seen any good materials on this, so if you have knowledge or pointers please let me know.
