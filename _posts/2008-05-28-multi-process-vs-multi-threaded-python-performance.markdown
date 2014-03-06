---
layout: parand
title:  "Multi-Process vs. Multi-Threaded Python Performance"
date:   2008-05-28 10:00:00
categories: say/index.php
---
Interesting benchmarks in [PEP 371 -- Addition of the Processing module to the standard library](/web/20101222040541/http://www.python.org/dev/peps/pep-0371/). In short, standard Python threads perform worse than non-threaded in almost every benchmark, while the multi-process Processing module generally does as you'd expect and reduces processing time proportional to the number of processors / cores.

You could argue this just means Python has a crappy thread implementation or that the benchmarks are biased, but it's interesting. I actually have an occasion for a multi-headed app, so perhaps I'll give Processing a try.

Via [Doug Hellmann](/web/20101222040541/http://blog.doughellmann.com/2008/05/pep-0371-adding-processing-module-to.html).
