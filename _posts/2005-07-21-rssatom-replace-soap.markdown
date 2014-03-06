---
layout: parand
title:  "On RSS/Atom replacing SOAP"
date:   2005-07-21 10:00:00
categories: say/index.php
---
Kurt Cagle has some interesting thoughts on [RSS/Atom as a replacement for SOAP](http://www.understandingxml.com/archives/2005/07/how_rssatom_is.html). He mentions WS vendors will likely poo-poo the idea, so I'm compelled as a reformed former vendor to comment.

I think Kurt makes excellent points. A lot of the Web is syndication oriented, and certainly RSS/Atom will be a better solution than SOAP for those cases. I generally agree that RSS/Atom will gain acceptance and be used in a variety of interesting places faster and wider than SOAP. In fact I just ran into a surprising one that will be unveiled to the public a bit later.

As Kurt says:

> If you make the syndication format too complex for people to use \(as I believe is the case with SOAP\) then they will migrate to simpler formats as they become available.

Agreed.

However, there's an important difference between SOAP and RSS/Atom that Kurt doesn't cover. Besides the basic complexity issue associated with SOAP, there's the issue of being able to process the data being passed around. The issue of encoding. This usually shows up as interop issues between toolkits, as well as in the XML-to-language-specific serialization / deserialization errors. It's part of what makes WSDL so complex \(although to be sure there are plenty of other factors\).

With SOAP, you have to get the payload very exactly right. Otherwise your consumer or producer will get very angry and spew bile all over you. The SOAP oriented world has attempted to specify encoding in the description \(WSDL\) and use it in the protocol \(SOAP\). The implementation hasn't been pretty. To this day it's still difficult to pass around something as simple as an array and be sure the various toolkits can handle it.

RSS and Atom basically punt on this point. They specify the framework for where to put your data and get out of the way. The actual content is a free for all. In Kurt's example, he declares it "text/xml", and goes on to put Job Control Language \(JCL\) in there. Nice.

How is the consumer to know that the contents are JCL, what JCL is, and how to handle it? RSS/Atom don't really say. There's the namespace declaration at the top, but that's about it. 

Compare this with WSDL/SOAP. Your WSDL would have to contain the schema for JCL. You'd likely break it up into methods. You'd figure out what the appropriate input/output for each method should be. Then you'd hope each toolkit calling your service produces exactly the XML you're looking for. If not, you'd get a nasty message telling you some bizarre looking thing could not serialize. 

So which is better? Specifying it exactly or making it a free for all?

To be fair, free for all is not a great description of what RSS/Atom lead to. It's better described as specifying the core information exchange framework and relying on existing/external means for understanding the specifics of the contents. At a base level, any RSS reader could read my feed and display it, if nothing else. No ugly serialization errors.

Now all the enterprise architects, the folks who do serious things with serious systems, the ones who frown and grimace to keep our country running, will tell you that we need law and order. We need specific specifications. We need to know exaclty what is in that payload, and by golly, if you can't get it right, you've got no business talking to business. 

So which is it? 

**For the Web, free for all is better**. As [smart](http://www.adambosworth.net/) [people](http://www.tbray.org/ongoing/) have said over and over, successful Web specifications are forgiving of errors. They're easy and forgiving. SOAP is trending towards neither of those. RSS and Atom will boldly go where SOAP should've gone if we'd done it better.
