---
layout: parand
title:  "XML Namespaces must die"
date:   2005-03-04 10:00:00
categories: stddev
---
I _hate_ XML namespaces. I strongly dislike them.

I will rant about this in detail in the future, as if there hasn't been enough
vitriol on this topic already. But let me present my current problem:

gsoap is returning this:

`  
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
`

Axis is the client, and doesn't like it. Complains of source-id not being
correct. Turns out, it has a problem with the namespace. Most SOAP servers
would return the result as:

` <updateOfferBidsResponse xmlns="urn:ows:cmoda:0.1">  
`

Note the inclusion of the namespace within this tag.

I looked thru the XML namespace tutorials, and I can tell this version means
the child nodes of updateOfferBidsResponse are in the namespace specified
here. But what does the gsoap version mean? Does

` <cmoda:updateOfferBidsResponse>`

also mean all children of updateOfferBidsResponse are in the cmoda namespace,
or are they in some other namespace? I'm no genius, but I've looked around a
bit and I can't find the answer. In any case, either the
[Axis](/web/20120203082040/http://ws.apache.org/axis/) or the
[gSOAP](/web/20120203082040/http://gsoap2.sourceforge.net/) folks didn't quite
get it either, or better yet, the XML libraries they're looking at got it
wrong or disagree.

I'm saying, people smarter than I don't get it.

I'm trackback'ing [Mr. Tim
Bray's](/web/20120203082040/http://www.tbray.org/ongoing/) long ago post in
case by some magic he becomes aware of this and sheds some light my way (he's
the co-author of the spec, and I've met him once or twice, so why not bother
him)…

##  7 Comments so far

  1. [Tim Bray](/web/20120203082040/http://www.tbray.org/ongoing/) on March 4th, 2005 

Who needs trackback when there's Technorati?

That message is completely hosed. First off, there's no header, there are a
couple of spurious instances of with no corresponding start-tag. Also you
declare the prefix as SOAP-ENV and then use as soap-ENV. There may be a
namespace problem here, but it's hiding behind a basic correctness problem.

  2. [Administrator](/web/20120203082040/http://www.parand.com/) on March 5th, 2005 

Hi Tim,  
This is great! Blogging works!  
Right, the message is hosed, but can you help with the basic question: does
including the namespace prefix on a tag inherit down to the children? Are the
children of updateOfferBidsResponse in the cmoda namespace or in some other?
In other words, does including a prefix have the same inheritence properties
as explicitly putting in the namespace as an attribute?  
Btw, I'm a big fan of everything else you've done outside of namespaces
![;-\)](/web/20120203082040im_/http://parand.com/say/wp-
includes/images/smilies/icon_wink.gif)

  3. [Administrator](/web/20120203082040/http://www.parand.com/) on March 5th, 2005 

I should also mention, true that the message is hosed in several ways, but
this appears specifically to be a namespace problem because if I change  
` <cmoda:updateOfferBidsResponse>  `
to  
` <updateOfferBidsResponse xmlns="urn:ows:cmoda:0.1″>  `
the rest of the message works.

The message is being produced by gSOAP, which tells me SOAP is too difficult,
which I will complain about later…

  4. [Tim Bray](/web/20120203082040/http://www.tbray.org/ongoing/) on March 15th, 2005 

Yes, when you declare a namespace prefix, that declaration applies to the tag
where it's declared and everything inside it. But it's not possible to have
any sensible further discussion until you debug the message so it's actually
XML, which it isn't at the moment.

  5. [Parand Darugar](/web/20120203082040/http://www.parand.com/) on March 15th, 2005 

I absolutely concede that this message is not in good shape; it's been through
a text editor, MS word, Outlook, and Wordpress, each of which has inflicted
its very own version of pain on it. I'll see if I can figure out how to attach
a file to a wordpress post so we get the actual valid XML on its own. It was
valid XML at one point, as verified by Xerces and XML Beans.

Putting that aside, let me make sure I understand what declaring a namespace
prefix means. Is it only when you include an xmlns attribute in your tag, or
does it also mean when you simply prefix your tag with the namespace? In other
words, in the fragment

` <ns:a>  `
<b />  
`</ns:a> `

a is not declaring a namespace, right? Further, the namespace identified by
"ns" does not get inherited by b simply because b is a child of a, right? If
the last statement is correct, then I believe misunderstanding this was
causing the problem with gsoap, which I believe was assuming the prefix on a
caused inheritence of that namespace by b.

  6. Dale Georg on March 17th, 2005 

Hey Tony! Pooya pointed to be your blog.
![:\)](/web/20120203082040im_/http://parand.com/say/wp-
includes/images/smilies/icon_smile.gif) I have to say I agree with you on
this. As I was telling Pooya, namespaces may be a good idea in theory, but in
practice they only serve to cause problems and be a pain in the butt.

  7. [Arun](/web/20120203082040/http://computinglife.wordpress.com/) on September 5th, 2007 

namespaces seems necessary from a logical point of view. But i asbolutely
agree the differences between implementations is a pain.

I'm currently trying the reverse - AXIS server with a gsoap client and its
paining me no end.

Do drop me a line if you have figured out how to get gsoap working with AXIS.

Posting your comment.

