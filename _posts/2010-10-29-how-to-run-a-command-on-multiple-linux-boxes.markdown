---
layout: parand
title:  "How To Run A Command On Multiple Linux Boxes"
date:   2010-10-29 10:00:00
categories: stddev
---
Here's a handy way of running a command on multiple boxes. In this case I wanted to check disk space on a series of machines.

Assuming you're using bash as your shell, the following will list the hostname and run df on machines racb13 through racb28 and spit out the results.
    
    
    for i in {13..28}; do ssh racb$i 'echo `hostname`; df -h | grep /data'; done
    
    
    
    

Note that ssh has to be setup to allow password-less login and so forth, but I'm assuming you're smart enough to know how to do that or can look it up.
