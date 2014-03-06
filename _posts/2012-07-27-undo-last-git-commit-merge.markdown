---
layout: parand
title:  "Undo last git commit / merge"
date:   2012-07-27 10:00:00
categories: stddev
---
Note to self: I quite stupidly merged and committed an unwanted branch into master. Took a surprisingly long time to figure out how to get rid of it:
    
    
    git reset --hard HEAD^
    

Which means reset git to one commit before the current head, effectively getting rid of the last commit.

Also, to undo a merge into master, you can reset back to origin/master with:
    
    
    git reset --hard origin/master
    

More scenarios for [undoing merges on this stackoverflow page](/web/20120924004657/http://stackoverflow.com/questions/2389361/git-undo-a-merge).
