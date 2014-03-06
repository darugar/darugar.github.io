---
layout: parand
title:  "Python itertools.groupby : a clearer example"
date:   2013-01-16 10:00:00
categories: stddev
---
itertools.groupby allows you to group a sorted list \(or any sorted iterable\) by some key, giving you the grouping key and the list of items grouped by that key.

For example, say you have a Django the model:
    
    
    class Item(models.Model):
        user     = models.ForeignKey( User, verbose_name="User", db_index=True )
        amount   = models.DecimalField( max_digits=19, decimal_places=2, default=0, null=True, blank=True )
    

 

And you want to group your Items by User. It'd be something like this:
    
    
    ordered_items = Item.objects.all().order_by('user')
    for user, item_list in itertools.groupby( ordered_items, lambda item: item.user ):
        print user, list(item_list)
    

 

That'll display the user, followed by all of the Items for that user, for each user.

Now let's say you wanted to display the user and the total amount for all of the items. You'd do something like this:
    
    
    ordered_items = Item.objects.all().order_by('user')
    for user, item_list in itertools.groupby( ordered_items, lambda item: item.user ):
        print user, sum( item.amount for item in item_list)
    

 
