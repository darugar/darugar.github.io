---
layout: parand
title:  "Access Python Dictionary Keys As Properties"
date:   2008-10-13 10:00:00
categories: stddev
---
Say you want to access the values if your dictionary via the dot notation instead of the dictionary syntax. That is, you have:
    
    
    d = {'name':'Joe', 'mood':'grumpy'}
    
    

And you want to get at "name" and "mood" via 
    
    
    d.name
    d.mood
    
    

instead of the usual 
    
    
    d['name']
    d['mood']
    
    

Why would you want to do this? Maybe you're fond of the Javascript Way. Or you find it more aesthetic. In my case I need to have the same piece of code deal with items that are either instances of Django models or plain dictionaries, so I need to provide a uniform way of getting at the attributes. 

Turns out it's pretty simple: 
    
    
    
    class DictObj(object):
        def __init__(self, d):
            self.d = d
    
        def __getattr__(self, m):
            return self.d.get(m, None)
    
    d = DictObj(d)
    d.name
    # prints Joe
    d.mood
    # prints grumpy
    
