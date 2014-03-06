---
layout: parand
title:  "Move Files Older Than X Days To Another Directory"
date:   2010-01-08 10:00:00
categories: stddev
---
Here's a little script for finding files modified more than 7 days ago and moving them to another directory:
    
    
    find . -type f -mtime +7 -print > /tmp/old_files.txt
    cat /tmp/old_files.txt | while read line; do mv "$line" ../old_files ; done
    
