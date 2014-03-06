---
layout: parand
title:  "Taste Vectors: Own, Share Your Tastes via XML"
date:   2005-03-10 10:00:00
categories: stddev
---
Each time you use Amazon it assembles a better profile of your tastes, your habits, your likes and dislikes. Why should they own your profile? I propose you publish your likes and dislikes via a simple XML format \(RSS? Atom?\), and we build collaborative filtering tools to help you find people who share your tastes and lead you to new things you'd like to taste. 

The basic idea is something like this: imagine we had a vector of likes and dislikes for a group of people. For each person, a long array that has a like or dislike for each item. We can use these vectors to calculate similarity between people's tastes, and to predict items they may like but have not tried. This sort of technology is fairly common now, with Amazon and Tivo being two  
well known examples. 

Trouble is, Amazon may have a partial picture of what I'm interested in based on my interactions with them, but they're not sharing it with me. So why don't I keep and publish my own taste vector? If you do the same, and we can convince many others to do the same, we can get some meaningful info floating out there.

Here's my basic proposal: let's come up with a dead-simple XML format for expressing these vectors, and a convention for where they live - say, http://yoursite/tastevector.xml . We need to agree on a couple of things: a consistent way of referring to items \(so we both use the same ID for the same item\), and a consistent way of expressing like and dislike. 

Consistent naming is a hard problem. So let's punt and go with a good-enough solution. We can use ISBN for books, IMDB ids for movies, Amazon id's for items carried by Amazon, and we'll figure out something for the rest. 

For expressing like and dislike, we can start with a very simple setup: _Like_, _Dislike_, _Neutral_, and _Own_, where _Own_ indicates you've bought this thing but haven't bothered to publish an opinion on it.

If you're a geek like me, we're pretty much there. But for the rest of the world, we'll need tools. This can be very simple - just a web page that lets you type in your item and your opinion of it, and spits back a piece of XML, or maybe updates your taste vector for you. This could be a service that stores and serves up your taste vector so you don't have to worry about it.

But now we're publishing lots of details about what people like. What about privacy? Well, come up with a fake name or a fake identity for your taste vector if you're worried about it. And don't list the items you'd be embarrassed to tell other people about.

With me so far? If we can get enough people to do this, a bunch of tools will emerge to gather intelligence from it and suggest new things for you to try. Believe me, this is data people would kill for - better yet, it's data marketers pay lots of money for today. 

Why do I care? Because my tastes are sometimes outside of the norm, and I want to find the other wierdos to turn me onto new wierd things to try. If you've been following the [long tail](/web/20101222050120/http://technorati.com/tag/long+tail) discussions, I may be able to convince you that there are a lot of outside-the-norm people there - in fact, it's very likely you are one yourself.

Why do I think this may work? Well, it'd take a miracle to get this to really go where it could, but the success of [technorati](/web/20101222050120/http://technorati.com/tag/technorati) style [folksonomies](/web/20101222050120/http://technorati.com/tag/technorati) has me thinking miracles are happening these days. 

If you've read this far you must be interested, so drop a comment in here and we can see if this has any legs…
