---
layout: parand
title:  "Queueing Benefits"
date:   2009-01-19 10:00:00
categories: stddev
---
Queues are nice things. We should be using more of them.

A couple of benefits that I knew of but didn't really appreciate until Alex started using beanstalkd in his application:

\- Having a worker-pulls-jobs-from-queue model provides near optimal use of the machine and prevents overload and thrashing. Setup as many simultaneous workers as your resources can handle and let them go. You have a controlled number of workers, preventing thrashing, and your workers work continuously. You don't have to worry about a load distribution strategy - workers pull jobs as fast as they can.

\- Provisioning new workers into the system becomes trivial. Want to add another box into the mix? Just set it up and have the workers start pulling jobs. You don't have to worry about registering the new box and getting it into the load distribution system - so long as it knows how to connect to the queue it can grab jobs. Alex commented that scaling his system is as easy as bringing up another virtual machine - as soon as it's up it starts pulling jobs.

These are both very important operational benefits that I had largely ignored.
