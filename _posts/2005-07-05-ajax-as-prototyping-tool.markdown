---
layout: parand
title:  "AJAX as Prototyping Tool"
date:   2005-07-05 10:00:00
categories: stddev
---
This is strange. I wanted to put together a simple UI for stepping thru large quantities of data. I'd have normally done this via [Tcl/Tk](/web/20101222040112/http://www.tcl.tk/) which provides a great environment for quick and dirty UIs, and has the added benefit that I'm very familiar with it.

But, as I went to download Tcl/Tk, it occurred to me that I could use AJAX. All I'm looking for is a simple screen that displays each record in turn. I can slap together the HTML page in no time. I can update the contents of the HTML page by simply slapping the values into javascript variables and eval'ing the result on the browser. Nice and easy.

I have to think thru the back-end capabilities a bit; it may get complicated navigating a very large record set controlled via the browser. If it does work out, it'll be a very nice separation of logic and UI.

But the main surprise for me was, I now consider AJAX simpler than Tcl/Tk for these types of tasks. Given that I complained about AJAX's learning curve earlier, I've had quite a change of heart.
