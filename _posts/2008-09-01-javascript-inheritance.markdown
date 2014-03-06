---
layout: parand
title:  "Javascript Inheritance"
date:   2008-09-01 10:00:00
categories: stddev
---
Javascript inheritance is another one of those topics that always escapes my mind, so I'm recording it here for future reference.

I tried to get into [Crockford's Prototypal Inheritance](/web/20101222052927/http://javascript.crockford.com/prototypal.html) method but I like the plain-old prototype inheritance without the object.create better. It's entirely possible that I'm not quite getting Crockford's method and its advantages; feel free to enlighten me by leaving a comment.

Anyway, here's what I'm going with: We'll have a base class \(actually an object\) English that says "hello" and "goodbye". We'll have a Spanglish class \(actually an object\) that inherits from English and says "ola" instead of "hello" \(over-rides the hello method\), but keeps saying "bye" \(inherits the bye method from English\).

The `Spanglish.prototype = new English\(\);` line does the actual inheritance by setting Spanglish's prototype to be an instance of English.
    
    
    function English() {
    	this.hello = function(){ return "hello"; }
    	this.bye   = function(){ return "bye"; }
    }
    
    function Spanglish() {
    	this.hello = function() { return "ola"; }
    }
    Spanglish.prototype = new English();
    
    e = new English();
    s = new Spanglish();
    
    e.hello();   // prints "hello"
    e.bye();     // prints "bye"
    s.hello();   // prints "ola"
    s.bye();     // prints "bye", inherited from English
    
