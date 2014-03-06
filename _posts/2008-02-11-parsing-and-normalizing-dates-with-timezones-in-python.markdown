---
layout: parand
title:  "Parsing and Normalizing Dates with Timezones in Python"
date:   2008-02-11 10:00:00
categories: stddev
---
This was a bit painful and not well documented, so documenting here for future reference.

Say you want to parse and normalize dates with timezones \(eg. dates in email headers, I believe based on rfc822\). Here's what you do:

Install [pytz](/web/20101222053903/http://pytz.sourceforge.net/).
    
    
    import email, time, datetime
    import pytz
    utctimestamp = email.Utils.mktime_tz(email.Utils.parsedate_tz( msg['Date'] ))
    utcdate= datetime.datetime.fromtimestamp( utctimestamp, pytz.utc )
    pacificdate = utcdate.astimezone(pytz.timezone('US/Pacific'))
    

parsedate\_tz produces a tuple that can be digested by mktime\_tz, which in turn spits out a timestamp based on the UTC timezone. You can turn this into a datetime via fromtimestamp and set its timezone to UTC. Once you have the TZ aware datetime you can manipulate it to your heart's content; the final line above converts it to a US/Pacific date. 

Full example: 
    
    
    >>> import email, time, datetime
    >>> import pytz
    >>> date_eastern = 'Thu, 31 Jan 2008 17:56:13 -0500'
    >>> utctimestamp = email.Utils.mktime_tz(email.Utils.parsedate_tz( date_eastern ))
    >>> utcdate= datetime.datetime.fromtimestamp( utctimestamp, pytz.utc )
    >>> utcdate
    datetime.datetime(2008, 1, 31, 22, 56, 13, tzinfo=<UTC>)
    utcdate.astimezone(pytz.timezone('US/Pacific'))
    datetime.datetime(2008, 1, 31, 14, 56, 13, tzinfo=<DstTzInfo 'US/Pacific' PST-1 day, 16:00:00 STD>)
    
