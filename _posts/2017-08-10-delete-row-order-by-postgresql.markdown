---
layout: post
title: "Delete some rows in SQL based on some order"
date:   2017-08-11 15:00:00 -0700
categories: Django
---
Recently I was working on optimization of query in PredictionIO. The prediction speed was incredibly slow due to uncleared cache of query histories. So our optimization was to keep the ten latest query groups and throw away all the older ones. So this operation involves some SQL that delete some rows based on a certain column (which is the query finish time here). Note that in PostgreSQL it's not allowed to use ORDER BY together with DELETE FROM. SO the trick is to use ctid, as the following code suggests:
{% highlight ruby %}
DELETE FROM $tableName
WHERE ctid IN (
SELECT ctid
FROM $tableName
ORDER BY finishtime
LIMIT $limit)
{% endhighlight %}
LIMIT is for how many rows we want to delete.
