---
layout: parand
title:  "Generating static html from markdown in python"
date:   2010-11-29 10:00:00
categories: say/index.php
---
Note to self, for future reference.

  * [Markdown reference](http://markdoc.org/ref/markup)

Generating static html:
    
    
    import markdown2
    file('classification.html','w').write( markdown2.markdown_path('classification.md', extras=["code-friendly"]) )
    
