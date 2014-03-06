---
layout: parand
title:  "Minimal Python HTTP Dispatch Server: simpledispatch"
date:   2006-11-30 10:00:00
categories: say/index.php
---
I was looking for a way to put together simple HTTP based services with as little fuss as possible. In this case that meant having a self contained script with minimal external dependencies, skipping even apache \(for various reasons such as not having root access on the box, not having apache installed, and just plain being lazy\).

I'm also generally interested in [script-only http servers](/web/20101222035722/http://www.parand.com/say/index.php/2005/12/20/script-only-http-servers/) and wanted to experiment.

Unfortunately I didn't immediately find anything that fit the bill, so I decided to hack something up. I'm fairly happy with the result. This is not intended to be a general purpose HTTP server; in fact, it's intended to be the opposite, serving small, specialized, self contained services. It doesn't serve static content \(files and images\); Apache and others do a great job of that already.

To use it, you simply define a function called _method\_yourmethod_ and add it to the handler, either by extending the base handler or by [monkey patching](/web/20101222035722/http://www.parand.com/say/index.php/2006/07/17/ruby-style-adding-methods-to-existing-classes-in-python/) it in. This method becomes accessible as http://yoursite/yourmethod . Parameters are passed to it by just adding more to the url path; for example: http://yoursite/yourmethod/param1/param2/param3 . These are received by _method\_yourmethod_ as a list.

Under the hood it uses introspection via getattr to find a method to match the URL, and passes it the remaining parameters.

The easiest way to understand it is to download the [simpledispatch.py](http://www.parand.com/say/misc/simpledispatch.py) file and look at the [use\_simpledispatch.py](http://www.parand.com/say/misc/use_simpledispatch.py) for usage examples. Run simpledispatch.py and access it at [http://localhost:8000/test/a/b/c](/web/20101222035722/http://localhost:8000/extended) . Run use\_simpledispatch.py and try it out at [http://localhost:8000/extended](/web/20101222035722/http://localhost:8000/extended) and [ http://localhost:8000/monkey](http://localhost:8000/monkey) .

Yes, I do know about the myriad wonderful frameworks out there \([django](/web/20101222035722/http://www.djangoproject.com/) is my framework of choice at the moment\) and I do know about [twisted](/web/20101222035722/http://twistedmatrix.com/trac/). simpledispatch is not a replacement for any of those; it's just a very simple dispatcher.
