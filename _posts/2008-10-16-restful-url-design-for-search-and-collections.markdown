---
layout: parand
title:  "RESTful URL Design For Search And Collections"
date:   2008-10-16 10:00:00
categories: stddev
---
I'm trying to find the appropriate design for RESTful design of URLs for search and for collections of items.

The setup: we have two models, Cars and Garages, where Cars can be in Garages. Base URLs:
    
    
    /car/xxx           (xxx = car id)
    /garage/yyy     (yyy = garage id)
    
    

Now we want to provide a search for cars - eg. show me all the blue sedans with 4 doors. What's the appropriate URL?
    
    
    1  - /cars/color/blue/type/sedan/doors/4
    2  - /cars/color:blue/type:sedan/doors:4
    3  - /cars/?color=blue&type=sedan&doors=4
    4  - /car/search/...
    
    

None of these are satisfying.

1 through 3 use "cars" as the base \(as opposed to "car"\). So the pattern for doing searches / collections would be to pluralize the model. This seems ok.

1 has arbitrary ordering of the fields and no good way to distinguish fields versus their values. 2 is slightly better, but still doesn't seem right.

3 uses the QUERYSTRING for the parameters instead of the PATHINFO, and frankly looks better to me, but I've heard of objections to using QUERYSTRING. The problem I have with it is it's not consistent - if I was searching on a single field my URL would probably be: `/cars/color/red` or something like that. Having the URL drastically change form just because there are more search parameters seems wrong.

4 uses the "car" base url along with the verb "search". That seems wrong - verbs shouldn't be part of the URL, right? It's been suggested several times though.

Now a slightly different case - let's find all the cars in a given garage:
    
    
    1  - /garage/yyy/cars
    2  - /cars/?garage=yyy
    
    

1 seems pretty good in this case.

Please chime in with your thoughts, either in the comments here or in the [Stackoverflow thread](/web/20101222040909/http://stackoverflow.com/questions/207477/restful-url-design-for-search).
