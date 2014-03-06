---
layout: parand
title:  "XML Namespaces must die"
date:   2005-03-04 10:00:00
categories: say/index.php
---
I _hate_ XML namespaces. I strongly dislike them.

I will rant about this in detail in the future, as if there hasn't been enough
vitriol on this topic already. But let me present my current problem:

gsoap is returning this:

```
<soap-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/"
xmlns:SOAP-ENC="http://schemas.xmlsoap.org/soap/encoding/"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:cmoda="urn:ows:cmoda:0.1">  
</soap><soap-ENV:Body>  
<cmoda:updateOfferBidsResponse>  
<setofresults>  
<item>  
<source-id>1</source>  
<sequence-num>1</sequence>  
<offer-id>123</offer>  
<success>true</success>  
<reason>CMODA-UPDATE-OFFER-BID-UNDEF</reason>  
</item>  
</setofresults>  
</cmoda>  
</soap>  
```

Axis is the client, and doesn't like it. Complains of source-id not being
correct. Turns out, it has a problem with the namespace. Most SOAP servers
would return the result as:

```
 <updateOfferBidsResponse xmlns="urn:ows:cmoda:0.1">  
```

Note the inclusion of the namespace within this tag.

I looked thru the XML namespace tutorials, and I can tell this version means
the child nodes of updateOfferBidsResponse are in the namespace specified
here. But what does the gsoap version mean? Does

```
<cmoda:updateOfferBidsResponse>
```

also mean all children of updateOfferBidsResponse are in the cmoda namespace,
or are they in some other namespace? I'm no genius, but I've looked around a
bit and I can't find the answer. In any case, either the
[Axis](/web/20120203082040/http://ws.apache.org/axis/) or the
[gSOAP](/web/20120203082040/http://gsoap2.sourceforge.net/) folks didn't quite
get it either, or better yet, the XML libraries they're looking at got it
wrong or disagree.

I'm saying, people smarter than I don't get it.

I'm trackback'ing [Mr. Tim Bray's](/web/20120203082040/http://www.tbray.org/ongoing/) long ago post in
case by some magic he becomes aware of this and sheds some light my way (he's
the co-author of the spec, and I've met him once or twice, so why not bother
him)

