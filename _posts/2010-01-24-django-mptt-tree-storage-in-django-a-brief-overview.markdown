---
layout: parand
title:  "Django-mptt: Tree Storage in Django: A Brief Overview"
date:   2010-01-24 10:00:00
categories: say/index.php
---
[django-mptt](/web/20120414080551/http://code.google.com/p/django-mptt/) is a library for storing tree oriented data using the Django ORM. It allows you to place your model instances into a tree structure and efficiently query for ancestors and children.

Here's a brief tutorial on how to use it:

After installing, you'll need to modify your model to include a "parent" field, and register it with mptt:
    
    
    class Person(models.Model):
        contact   = models.ForeignKey( Contact, db_index=True )
        role      = models.CharField(max_length=20, blank=True)
        parent    = models.ForeignKey('self', null=True, blank=True, related_name='children')
    
        def __unicode__(self):
            return "Person: <%s>" % (self.contact.email, )
    
    mptt.register(Person)
    

mptt dynamically adds fields to your model, so you'll need to syncdb after you've added the parent attribute and the mptt.register call to your model.

The basics are fairly easy to use:

To move a node to the root of the tree, use move\_to with a targe of None:
    
    
    person1.move_to(None)
    person1.save()
    

To make a node the child of another, set its parent:
    
    
    person2.parent = person1
    person2.save()
    

To find the children of a node, use the children field:
    
    
    >>>person1.children.all()
    [<Person: Person: <[[email protected]](/web/20120414080551/http://cloudflare.com/email-protection.html)>>, <Person: Person: <[[email protected]](/web/20120414080551/http://cloudflare.com/email-protection.html)>>]
    

Here's a little snippet of code to setup a 15 node tree where each node has two child nodes:  
  
\[UPDATE\] The code in this snippet is not correct - you have to save each node as you update it, then look it up again. You can't modify a node, save it, then use the reference you already have for it. I'll update the code when I get a chance
    
    
    contacts = []
    people = []
    for n in range(15):
        c = mod.Contact(email="test" + str(n) + "@testing.com")
        c.save()
        contacts.append(c)
        p = mod.Person(contact=c)
        p.save()
        people.append(p)
    
    people[0].move_to(None)  # Root
    people[0].save()
    for n in range(1,15):
        people[n].parent = people[(n-1)/2]
        people[n].save()
    

Now let's take a look around:
    
    
    >>>people[7].parent
    <Person: Person: <[[email protected]](/web/20120414080551/http://cloudflare.com/email-protection.html)>>
    
    >>>people[3].children.all()
    [<Person: Person: <[[email protected]](/web/20120414080551/http://cloudflare.com/email-protection.html)>>, <Person: Person: <[[email protected]](/web/20120414080551/http://cloudflare.com/email-protection.html)>>]
    

Now let's move things around a bit; we'll take person3, which is 2 levels down from the root, and make it a direct child of the root:
    
    
    >>>people[3].parent = people[0]
    >>>people[3].save()
    
    >>>people[0].children.all()
    [<Person: Person: <[[email protected]](/web/20120414080551/http://cloudflare.com/email-protection.html)>> <Person: Person: <[[email protected]](/web/20120414080551/http://cloudflare.com/email-protection.html)>>, <Person: Person: <[[email protected]](/web/20120414080551/http://cloudflare.com/email-protection.html)>>]
    

And we can look at the ancestors of a given node:
    
    
    people[14].get_ancestors()
