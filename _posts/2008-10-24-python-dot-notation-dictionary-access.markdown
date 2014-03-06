---
layout: parand
title:  "Python Dot Notation Dictionary Access"
date:   2008-10-24 10:00:00
categories: stddev
---
In most cases I prefer dot notation over bracket notation for dictionary access. That is, I prefer `mydictionary.myfield` over `mydictionary\['myflield'\]`. I also prefer attempted access to undefined keys to return None instead of raising an exception.

With the help of [this thread](/web/20101222041208/http://stackoverflow.com/questions/224026/javascript-style-dot-notation-for-dictionary-keys-unpythonic), this is what I've been using:
    
    
    
    class dotdict(dict):
        def __getattr__(self, attr):
            return self.get(attr, None)
        __setattr__= dict.__setitem__
        __delattr__= dict.__delitem__
    
    >>> dd = dotdict()
    >>> dd.a
    >>> dd.a = 'one'
    >>> dd.a
    'one'
    >>> dd.keys()
    ['a']
    
    >>> existing = {'a':'A', 'b':'B'}
    >>> dot_existing = dotdict(existing)
    >>> dot_existing.a
    'A'
    
    
