---
layout: parand
title:  "jQuery serializeArray: Why Not An Associative Array?"
date:   2008-07-08 10:00:00
categories: say/index.php
---
I'm trying to examine and modify form variables from jQuery by catching the submit event. jQuery has a serializeArray method that hands you the form variables in a nice array. For example:
    
    
    	$('#someform').submit( function() {
    		$.post("/some/url/", $(this).serializeArray(),
    			function(data){
    			    console.log(data);
    			}, "json");
    		return false;
    	 } );
    

This is great, but the result of serializeArray is an integer indexed array whose values are \(key,value\) pairs. Eg.
    
    
    	var data = $(this).serializeArray(),
    	console.log( data[0] );
    >> output: Object name=somename value=537
    

I'm wondering why the array looks like this, instead of being a dictionary \(associate array, hash, or whatever you want to call it\) such that the keys are "name"s and values are "value"s. Eg.
    
    
    	var data = $(this).serializeArray(),
    	console.log( data.somename );
    >> output: 537
    

Anybody know the answer?
