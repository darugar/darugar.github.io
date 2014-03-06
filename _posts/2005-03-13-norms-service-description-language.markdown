---
layout: parand
title:  "Norm&#8217;s Service Description Language"
date:   2005-03-13 10:00:00
categories: stddev
---
Check it out: [http://norman.walsh.name/2005/03/12/nsdl](/web/20110106035935/http://norman.walsh.name/2005/03/12/nsdl) .

I like it a lot. **Specifying the parameters via XPath statements is dead on**. The POST body as template is also excellent, although I'm not crazy about the syntax. How do you feel about expressing the input parameters as XPath too? So maybe the XML fragment, with the parts that should be filled in specified separately as XPath. XPath is not just for selecting; it can get you to the element you want to fill in or modify as well.

I'm trying to think back to my own attempt at creating a description language circa 2000. I believe I used actual XML fragments, ala Norm's POST method, for all pieces, so you could simply copy the XML out of the description language, massage to taste, and send it on its way. The response was also expressed as a sample XML in the description file, although I do like Norm's better. 

I didn't have any typing information in there, and I think that's a plus. I know all the strongly-typed Java folks will be shocked, but scripting languages have lived and prospered without typing \(everything's a string\) for some time. 

What value does typing have? Information \(telling the consumer what to send in\), and Validation \(letting the consumer check his parameters before sending\). I'd argue once you have something that's appropriate for validation, it's complex enough to lose its informational value for the vast majority of people out there. The only validation language I've seen have usefulness is regexp, and that's tool complex for most people to read and understand. So skip it; put the parameter types in a human readable document. Ok, so maybe RELAX NG is nice, and I can understand it if I crease my forehead, hold my breath, and concentrate, but most people don't like creasing their foreheads.

Most of the work is not in checking the syntax of the parameters anyway; it's in the semantics. Calling the Amazon service was nice and easy, except I had to figure out what all their categories and nomenclature meant. Schema's not going to help me with that.

Nice work Norm.
