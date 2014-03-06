---
layout: parand
title:  "Titanium Studio: How To View Android Log Messages"
date:   2011-08-15 10:00:00
categories: say/index.php
---
Apparently with Titanium Studio it's not possible to see log messages in the Titanium console.

Here's how you see your log messages:
    
    
    adb logcat | grep "TiAPI"
    

adb is in the tools directory of your Android sdk.
