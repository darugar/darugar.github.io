---
layout: parand
title:  "Experiences with DabbleDB?"
date:   2006-11-02 10:00:00
categories: say/index.php
---
I've been interested in [DabbleDB](/web/20101222035742/http://dabbledb.com/) for some time now, since they first showed up on the scene with their [Under The Radar](http://dabbledb.com/explore/7minutedemo/) demo. I immediately pointed a friend at them, who in turn got very excited and spent a few days integrating his app with theirs, only to give up as he hit scaling issues on the DabbleDB side \(his data set was too large\).

I took another look, prompted by [Jon Udell's latest screencast](http://weblog.infoworld.com/udell/screenroom/dabble_flv.html) \(via [Kedrosky](/web/20101222035742/http://paul.kedrosky.com/archives/2006/11/01/jon_udell_visit.html)\), and I understand better what they're going after. Seems they're targeting small business, where DabbleDB is used as a stand-alone app, very much as Excel on the Web with sharing built in.

I could see that working for them, although the install base and more importantly experience base around Excel is a tough nut to crack. And then there is [Google Docs](/web/20101222035742/http://docs.google.com/) of course, which is not nearly as rich of an experience, but if the use case is excel-on-the-web-with-sharing, it may be good enough.

But for me the more interesting side is being able to "mash up" DabbleDB into my own app. I have several side projects where having a nice tabular view that could explode out into the rich experience that Dabble offers would be fantastic. You're using my Web app, you come to a nice innocent looking table, you click on it, and you have all the power of Dabble underneath. I love the idea of being able to build multiple views in DabbleDB and offer them as pages in my app - I'd get a much richer experience in my app without having to build the backend and the UI for the data parts.

However, as it stands the UI is not easily transplantable into my app. The data is offered out in reasonable ways, via an API and RSS, but I already have the data. I'm interested in DabbleDB the app. I don't think I can host my apps on Dabble, nor can I integrate the Dabble interface into into my app.

DabbleDB could be my online database in a cloud. I can interact with my data via APIs, which is very nice. However, given that Dabble is a startup, do I really want to trust them with my data?

Funny how that works - with [Amazon's S3](/web/20101222035742/http://www.amazon.com/S3-AWS-home-page-Money/b/ref=sc_fe_l_2/102-0987217-3863349?ie=UTF8&node=16427261&no=3435361&me=A36L942TSJ2AJA) I have the opposite reaction. I'd like to back up all my data to it, because being in Amazon's data center gives me a feeling of security. There's also Google Base, but Google is starting to creep me out with their data policies and their [customer support](/web/20101222035742/http://www.parand.com/say/index.php/2005/12/13/adsense-login-nonsense/) \(disclosure: I work at Yahoo\!, but they started creeping me out before I started a Yahoo\!\).

So let's forget mashups and go back to the shared-online-excel use case. Recently I was exchanging data with the business folks and ran into a dataset that would be nicely served by DabbleDB: the query and report capabilities would be very useful, as would online collaboration. But I don't think that would work either: I seriously doubt corporate policy would allow me to host confidential data on external servers. I realize there's plenty of data in the world that doesn't need to be secured, but that excludes pretty much all business / corporate data in any reasonably sized company.

Maybe I'm just not the target audience for DabbleDB at the moment. But I'd like to be. I like the app and I like the idea. I'd like to find a way to use it.

Have you had experience with DabbleDB or other hosted apps? What do you think?
