---
layout: parand
title:  "How To Dynamically Select Part of a jQuery Call Chain"
date:   2008-05-07 10:00:00
categories: say/index.php
---
Updated, thanks to [Simon Willison](/web/20101222040651/http://simonwillison.net/):

Say you'd like to pick part of your jQuery call chain dynamically - for example, to removeClass for many elements, but addClass to one special element. Here's how you do it:
    
    
    var myfunc = some_condition ? 'addClass' : 'removeClass';
    $('#someid').html('something')[myfunc]('some_class');
    

The first line selects the function name as a string. The second line calls the 'html' function \(it could be any function; html is just the example in this case\), followed by the function with the selected name \(addClass or removeClass in this case\). 

You'd probably use this in the context of a loop, eg:
    
    
    for (var i=0; i<10; i++) {
        var myfunc = some_condition ? 'addClass' : 'removeClass';
        $('#something'+ i).html('sample text ' + i)[myfunc]('selected');
    }
    
