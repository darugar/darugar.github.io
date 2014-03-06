---
layout: parand
title:  "Bug Labs: Good Stuff"
date:   2008-03-06 10:00:00
categories: stddev
---
![Bug Labs Logo](/web/20101222033653im_/http://www.buglabs.net/images/nav/logo.gif?1202843410)

I caught Peter Semmelhack's talk at ETech and also had a chance to chat with him and [Mershad](/web/20101222033653/http://www.buglabs.net/users/mehrshad) over lunch. [Bug Labs](/web/20101222033653/http://www.buglabs.net/) sounded interesting - an open hardware platform where functionality can be added as modules, almost like connecting legos together. But it turns out there's more to it than that.

Bug labs also deals with the programming interface for the devices and sensors, abstracting the functionality as web services. The device runs its own on-board web server, so getting an image from the camera is as easy as going to the url for the for the camera on the device - something like http://deviceaddress/service/camera . Apparently it implements OSGI, which would allow automated discovery and such \(I'm a bit surprised they used OSGI in this context actually, but it does make sense\).

I think the form factor is going to be very important - a physical device has to be physically appealing. The bug is not unattractive, but it's not going to be as small or convenient as a purpose-built device. On the other hand, as Peter mentioned, there are lots of niches for devices that aren't mass market \(eg. devices for the blind\) that the Bug could address.

I initially thought the main appeal was the modularity and ability to add sensors, but I think the open programming interface might be a bigger deal. Imagine a cell phone \(or GPS device\) that you had full programmable access to. Looks like this would be a fun thing to play with.
