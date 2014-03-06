---
layout: parand
title:  "Handy Javascript Scoping Trick"
date:   2008-05-06 10:00:00
categories: say/index.php
---
Neat [Javascript function scoping trick from Dustin Diaz](/web/20101222040408/http://www.dustindiaz.com/scoping-anonymous-functions/), master of cool Javascript tricks. His Javascript Video Tutorials were the first time I was exposed to proper Javascript \(Justin, do some more\!\).

Here's the trick:
    
    
    var o = 'hello world';
    
    (function() {
      alert(this);
    }).call(o);
    

And why is this neat? Because it lets you avoid the "that = this" funkiness \(if you've had to do it you know what I'm talking about\). Read Justin's post for actual info.
