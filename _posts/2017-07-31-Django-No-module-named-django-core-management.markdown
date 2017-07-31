---
layout: post
title: "Solutions to Django No module named django.core.management issue for general and Vagrant users"
date:   2017-07-31 14:58:00 -0700
categories: Django
---
In Django, when running the file './manage.py', such as "./manage.py", you may experience the following error:
{% highlight ruby %}
File ./manage.py, line 8, in <module>
     from django.core.management import execute_from_command_line
ImportError: No module named django.core.management
{% endhighlight %}

This post at [StackOverflow](https://stackoverflow.com/questions/30389771/importerror-no-module-named-django-core-management-when-using-manage-py) covers a few general possible reasons for this issue. Here I'd like to add some details for the case where Vagrant is used as the virtual environment for Django development:

To enter Vagrant virtual env, first run 'vagrant up' if it's not up already. Then 'vagrant ssh'. Now we're in the Vagrant virtual env. 
