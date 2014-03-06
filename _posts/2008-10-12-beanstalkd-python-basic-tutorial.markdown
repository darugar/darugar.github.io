---
layout: parand
title:  "Beanstalkd / Python Basic Tutorial"
date:   2008-10-12 10:00:00
categories: say/index.php
---
\(First [install beanstalkd and pybeanstalk](/say/index.php/2008/10/12/setting-up-beanstalkd-on-ubuntu-for-python.html)\)

Beanstalkd is an in-memory queuing system. It supports named queues \(called 'tubes'\), priorities, and delayed delivery of messages.

Terminology: a message is called a _job_, and queues are called _tubes_.

Let's look at an example scenario. Say you want to create 2 tubes, one called "orders" and another called "emails", place orders into the first tube \(or queue\) and emails into the second, and have different processes handle orders and emails.

You can create queues by simply naming and putting messages into them. On the producer side:
    
    
    from beanstalk import serverconn
    c = serverconn.ServerConn('localhost', 99988)
    
    # put a message (or job) into the default queue:
    c.put('first message, into default tube')
    
    # now start using a named tube:
    c.use('orders')
    c.put('second message, into orders tube')
    

Now on the consumer:
    
    
    from beanstalk import serverconn
    c = serverconn.ServerConn('localhost', 99988)
    
    # by default your connection will be listening on the 'default' tube.
    # switch it to use the 'orders' tube.
    # This should return the 'orders' message and ignore the 'default' message:
    c.watchlist = ['orders']
    j = c.reserve()
    print j
    # {'data': 'second message, into orders tube', 'jid': 39, 'bytes': 32, 'state': 'ok'}
    

You can similarly setup another consumer to listen on only the 'emails' tube, or both, or any other scenario you want.

Beanstalkd also supports priorities, with 0 being highest priority and higher numbers meaning lower priority. You define message priority with:
    
    
    c.put('low priority message', pri=999 )
    c.put('high priority message', pri=0 )
    
    j = c.reserve()
    print j
    # {'data': 'high priority message', 'jid': 41, 'bytes': 21, 'state': 'ok'}
    # the high priority message was delivered before the low priority message, even
    # though the low priority message was first into the queue
    

The beanstalkd consumption model is to "reserve" a message \(or job\), process it, and then tell beanstalkd you've successfully dealt with the message so it can be thrown away. When you first get the job via c.reserve\(\) you haven't actually fully consumed it; you've just reserved it for processing.

What does this mean? Imagine a scenario where you reserve a message but your process dies before you have a chance to fully process it. Beanstalkd holds your message in reserve for a period of time, but since it hasn't heard from you confirming you've successfully dealt with the message, it eventually removes the reservation and makes the message available once again for the next consumer to grab. This is a basic handshake between the consumer and the server to allow for some level of resiliency.

So once you're finished dealing with the message you've reserved, be sure to "delete" it, letting the beanstalkd server know it can throw that message away:
    
    
    j = c.reserve()
    # do some processing with j
    c.delete(j['jid'])
    

So there you have the basics. Let me know if you're interested and I can cover a few more topics.
