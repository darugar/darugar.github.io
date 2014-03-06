---
layout: parand
title:  "Pig (Hadoop) Commands And Sample Results"
date:   2008-06-19 10:00:00
categories: say/index.php
---
I find seeing the results of [Pig](/web/20101222043006/http://incubator.apache.org/pig/) commands on sample data a good companion to the [PigLatin language reference](/web/20101222043006/http://wiki.apache.org/pig/PigLatin), so I setup some simple sample data and ran commands, capturing the results.Here's the sample data as well as the commands:

**/data/one:**
    
    
    a	A	1
    b	B	2
    c	C	3
    a	AA	11
    a	AAA	111
    b	BB	22
    

**/data/two:**
    
    
    x	X	a
    y	Y	b
    x	XX	b
    z	Z	c
    

**Pig commands and their results:**
    
    
    one = load 'data/one' using PigStorage();
    two = load 'data/two' using PigStorage();
    
    generated = FOREACH one GENERATE $0, $2;
    (a, 1)
    (b, 2)
    (c, 3)
    (a, 11)
    (a, 111)
    (b, 22)
    
    grouped = GROUP one BY $0;
    (a, {(a, A, 1), (a, AA, 11), (a, AAA, 111)})
    (b, {(b, B, 2), (b, BB, 22)})
    (c, {(c, C, 3)})
    
    grouped2 = GROUP one BY ($0, $1);
    ((a, A), {(a, A, 1)})
    ((a, AA), {(a, AA, 11)})
    ((a, AAA), {(a, AAA, 111)})
    ((b, B), {(b, B, 2)})
    ((b, BB), {(b, BB, 22)})
    ((c, C), {(c, C, 3)})
    
    summed = FOREACH grouped GENERATE group, SUM(one.$2);
    (a, 123.0)
    (b, 24.0)
    (c, 3.0)
    
    counted = FOREACH grouped GENERATE group, COUNT(one);
    (a, 3)
    (b, 2)
    (c, 1)
    
    flat = FOREACH grouped GENERATE FLATTEN(one);
    (a, A, 1)
    (a, AA, 11)
    (a, AAA, 111)
    (b, B, 2)
    (b, BB, 22)
    (c, C, 3)
    
    cogrouped = COGROUP one BY $0, two BY $2;
    (a, {(a, A, 1), (a, AA, 11), (a, AAA, 111)}, {(x, X, a)})
    (b, {(b, B, 2), (b, BB, 22)}, {(y, Y, b), (x, XX, b)})
    (c, {(c, C, 3)}, {(z, Z, c)})
    
    flatc = FOREACH cogrouped GENERATE FLATTEN(one.($0,$2)), FLATTEN(two.$1);
    (a, 1, X)
    (a, 11, X)
    (a, 111, X)
    (b, 2, Y)
    (b, 22, Y)
    (b, 2, XX)
    (b, 22, XX)
    (c, 3, Z)
    
    joined = JOIN one BY $0, two BY $2;
    (a, A, 1, x, X, a)
    (a, AA, 11, x, X, a)
    (a, AAA, 111, x, X, a)
    (b, B, 2, y, Y, b)
    (b, BB, 22, y, Y, b)
    (b, B, 2, x, XX, b)
    (b, BB, 22, x, XX, b)
    (c, C, 3, z, Z, c)
    
    crossed = CROSS one, two;
    (a, AA, 11, z, Z, c)
    (a, AA, 11, x, XX, b)
    (a, AA, 11, y, Y, b)
    (a, AA, 11, x, X, a)
    (c, C, 3, z, Z, c)
    (c, C, 3, x, XX, b)
    (c, C, 3, y, Y, b)
    (c, C, 3, x, X, a)
    (b, BB, 22, z, Z, c)
    (b, BB, 22, x, XX, b)
    (b, BB, 22, y, Y, b)
    (b, BB, 22, x, X, a)
    (a, AAA, 111, x, XX, b)
    (b, B, 2, x, XX, b)
    (a, AAA, 111, z, Z, c)
    (b, B, 2, z, Z, c)
    (a, AAA, 111, y, Y, b)
    (b, B, 2, y, Y, b)
    (b, B, 2, x, X, a)
    (a, AAA, 111, x, X, a)
    (a, A, 1, z, Z, c)
    (a, A, 1, x, XX, b)
    (a, A, 1, y, Y, b)
    (a, A, 1, x, X, a)
    
    SPLIT one INTO one_under IF $2 < 10, one_over IF $2 >= 10;
    -- one_under:
    (a, A, 1)
    (b, B, 2)
    (c, C, 3)
    
    
