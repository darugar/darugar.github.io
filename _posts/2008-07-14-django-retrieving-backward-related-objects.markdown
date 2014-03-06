---
layout: parand
title:  "Django: Retrieving Backward Related Objects"
date:   2008-07-14 10:00:00
categories: stddev
---
Another one in the category of always-forget-how-to-do-this-so-noting-here:
    
    
    class Entry(models.Model):
        blog = models.ForeignKey(Blog)
    
    b = Blog.objects.get(id=1)
    b.entry_set.all() # Returns all Entry objects related to Blog.
    
    # b.entry_set is a Manager that returns QuerySets.
    b.entry_set.filter(headline__contains='Lennon')
    b.entry_set.count()
    

Full docs [here](/web/20101222050110/http://www.djangoproject.com/documentation/db-api/#backward).
