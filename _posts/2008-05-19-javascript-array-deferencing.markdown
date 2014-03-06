---
layout: parand
title:  "Javascript Array Deferencing?"
date:   2008-05-19 10:00:00
categories: say/index.php
---
I have an array, say:
    
    
    var pieces = [2008, 5, 19, 13, 49];
    

I'd like to create a date based on this; the equivalent of:
    
    
    new Date( 2008, 5, 19, 13, 49 );
    

Is there a way to do that in Javascript? Can I dereference the array in my date create call? I'd prefer to avoid eval.
