---
layout: parand
title:  "Django: Using The Permission System"
date:   2010-02-19 10:00:00
categories: stddev
---
I was surprised at how little information I found on making use of Django's permission system. Here are some quick notes on one way to use it:

_Groups_ are groups of users. For example, you could define a group of users who have premium accounts, or have been verified in some way, or are somehow special:
    
    
    from django.contrib.auth.models import Group, Permission
    special_users = Group(name='Special Users')
    special_users.save()
    really_special_users = Group(name='Super Special Users')
    really_special_users.save()
    

Now you have two groups defined and can define permissions for them. Django associates permissions with models \(note: not model instances, but models\). You'll need to select a model to apply the permissions to, and do a small dance with "ContentType" to find that model's content type:
    
    
    from django.contrib.contenttypes.models import ContentType
    somemodel_ct = ContentType.objects.get(app_label='myapp', model='somemodel')
    
    can_view = Permission(name='Can View', codename='can_view_something',
                           content_type=somemodel_ct)
    can_view.save()
    
    can_modify = Permission(name='Can Modify', codename='can_modify_something',
                           content_type=somemodel_ct)
    can_modify.save()
    

You've now defined two permissions and can associate them with your Groups:
    
    
    special_users.permissions.add(can_view)
    really_special_users.permissions = [can_view, can_modify]
    

Our groups and their associated permissions are ready to go. Now we just have to associate these permissions with users:
    
    
    jack=User.objects.get(email='[[email protected]](/web/20120325165629/http://cloudflare.com/email-protection.html)')
    jack.groups.add(special_users)
    
    jill=User.objects.get(email='[[email protected]](/web/20120325165629/http://cloudflare.com/email-protection.html)')
    jill.groups.add(really_special_users)
    

We're all done. Now we can check the users' permissions:
    
    
    >>> jack.has_perm('myapp.can_view_something')
    True
    >>> jack.has_perm('myapp.can_modify_something')
    False
    
    >>> jill.has_perm('myapp.can_view_something')
    True
    >>> jill.has_perm('myapp.can_modify_something')
    True
    

And to use it in your templates:
    
    
    {% if perms.myapp.can_view_something %}
    Here is something for you to see.
    {% else %}
    Can't show you!
    {% endif %}
    
