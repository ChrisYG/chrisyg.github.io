---
layout: post
title: "Drop all tables with a common name prefix in PostgresQL"
date:   2017-08-01 14:43:00 -0700
categories: Django
---
Today I was working on PostgresQL database cleanup for our predictive server, which might speed up the prediction by some degree. So a major task was to drop all tables that contained data sent to each engine and were all named as "pio_event_1", "pio_event_2", ... "pio_event_eventIdHere".

It's easy to drop one table using "DROP TABLE pio_event_1", but obviously it's hard to manually repeat for hundreds of events. At first I was trying to do this elegantly, hopefully in one single step, using a for loop through select query results, but unfortunately in PostgresQL we can't run it as plain SQL, since FOR is a construct in the plpgsql procedural language, and we need to put this into a plpgsql function, which I feel is unnecessary for a simple task as dropping some tables. (Reference: https://www.postgresql.org/message-id/14344.1293073542%40sss.pgh.pa.us).

Thus I decided to do it just inelegantly yet more straightforwardly:
first, I ran the following query to get a sequence of DROP queries that I need to run later:
{% highlight ruby %}
SELECT 'DROP TABLE ' || TABLE_NAME || ';'
FROM INFORMATION_SCHEMA.TABLES
WHERE TABLE_NAME LIKE 'pio_events%'
{% endhighlight %}
(Note how PostgresQL uses '||' to concat, instead of '+')
This query resulted in:
{% highlight ruby %}
"DROP TABLE pio_event_106"
"DROP TABLE pio_event_164"
"DROP TABLE pio_event_12"
"DROP TABLE pio_event_22"
"DROP TABLE pio_event_25"
"DROP TABLE pio_event_26"
"DROP TABLE pio_event_2"
"DROP TABLE pio_event_3"
"DROP TABLE pio_event_4"
"DROP TABLE pio_event_5"
{% endhighlight %}
Then all we need to do is just removing all quotes in the output with replace in either an text editor or pgAdmin, and copy all the DROP queries to anywhere you'd like to run them.
