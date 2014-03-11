---
layout: parand
title:  "How To Dynamically Import Python Modules"
date:   2012-01-11 10:00:00
categories: say/index.php
---
Here's how you import a python module dynamically: say your module is called "mysettings" and it's in the directory "config". Make sure you have a `__init__.py` in your "config" directory and use:
    
    
    mysettings = __import__("config.mysettings", fromlist=["config"])
    
    

This is equivalent to
    
    
    from config import mysetings
    
