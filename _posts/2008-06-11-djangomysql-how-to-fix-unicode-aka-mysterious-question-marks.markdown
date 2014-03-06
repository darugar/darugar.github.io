---
layout: parand
title:  "Django+MySQL: How To Fix Unicode (aka Mysterious Question Marks)"
date:   2008-06-11 10:00:00
categories: say/index.php
---
If you're running into the problem where unicode items in your Django / MySQL project are displayed as question marks, here's the likely problem and solution, found in this [django-users thread](/web/20101222043056/http://groups.google.com/group/django-users/browse_thread/thread/a9b53db451aa4590/0b99a2f071cc4404#0b99a2f071cc4404):

The likely problem is that your MySQL encoding is set to latin1, as opposed to utf8. You can check this via:
    
    
     mysqld --verbose --help | grep character-set
    

You'll probably see:
    
    
    character-set-server              latin1
    

You want this to be uft8. To modify it, edit your my.conf file \( /etc/mysql/my.conf on ubuntu \), adding the following lines to the appropriate sections:
    
    
    [client]
    ...
    default-character-set = utf8
    
    [mysqld]
    ...
    character-set-server=utf8
    collation-server=utf8_unicode_ci
    init_connect='set collation_connection = utf8_unicode_ci;'
    

Now restart mysql:
    
    
    sudo /etc/init.d/mysql restart
    

And alter your existing tables to use the utf8 encoding:
    
    
    mysql your_db_name
    
    alter table your_table_name convert to character set utf8;
    

And that should do it. 
