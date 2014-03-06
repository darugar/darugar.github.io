---
layout: parand
title:  "Using Django Signals To Watch For Changes To Instances"
date:   2008-06-11 10:00:00
categories: stddev
---
Say you want to monitor changes to instances of a model and update something based on the changes. In my example I wanted to maintain a sum of the values that had certain characteristics. You can accomplish this with [Django Signals](/web/20101222043406/http://code.djangoproject.com/wiki/Signals).

Signals are events that fire at various pre-defined moments - for example, before an instance is saved, after it's saved, etc. You can subscribe to these events, allowing your callback handler to be called at those moments.

The code below subscribes to the _post\_init_ and _post\_save signals_. _post\_init_ gets triggered when a model's \_\_init\_\_ class is done executing, which generally means when a model instance is created for the first time or instantiated from a query to the DB. This is actually too frequent for the use case I have in mind \(checking the before-modification and after-modification values of certain fields\), but seems to be the only place I can hook in to get the pre-modification values.

_post\_init_ gets triggered after the instance is saved to the DB. The code below stores the pre-modification values in _pre\_save_ when it gets triggered by the _post\_init_ signal, and checks them against the post-modification values when it gets triggered by the _post\_save_ signal.

Note that you'll probably want to clean up _pre\_save_ periodically. Unfortunately _post\_init_ and _post\_save_ are not symmetrical \(you'll get a _post\_init_ anytime an instance is created, for example when you query the DB\), so you can't simply delete from _pre\_save_ when the _post\_save_ signal gets triggered.
    
    
    from django.dispatch import dispatcher
    from django.db.models import signals
    
    pre_save = {}
    
    def change_watcher(sender, instance, signal, *args, **kwargs):
        print "SIGNAL:", sender, instance.report, signal, args, kwargs
        if signal == signals.post_init:
            pre_save[instance.id] = (instance.field1, instance.field2)
        else:
            if pre_save[instance.id][0] != instance.field1:
                print "Changed field1"
            if pre_save[instance.id][1] != instance.field2:
                print "Changed field2"
    
    for signal in (signals.post_init, signals.post_save):
        dispatcher.connect(change_watcher, sender = Expense, signal = signal)
    
