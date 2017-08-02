---
layout: post
title: "Cannot deserialize the current JSON object when using PredictionIO batch import"
date:   2017-08-01 14:43:00 -0700
categories: Django
---
Today I was working on getting the PredictionIO batch import to work on our BPM backend. At line {% highlight ruby %} return JsonConvert.DeserializeObject<T>(responseJson); {% endhighlight %}, an error occurred:

{% highlight ruby %}
Cannot deserialize the current JSON object (e.g. {"name":"value"}) into type 'some type' because the type requires a JSON array (e.g. [1,2,3]) to deserialize correctly. To fix this error either change the JSON to a JSON array (e.g. [1,2,3]) or change the deserialized type to an array or a type that implements a collection interface (e.g. ICollection, IList) like List<T> that can be deserialized from a JSON array. JsonArrayAttribute can also be added to the type to force it to deserialize from a JSON array.
{% endhighlight %}

In debugging mode I took a look at the 'responseJson' variable returned from PredictionIO:
{% highlight ruby %}
"[{\"status\":201,\"eventId\":\"d03c9bqefba24342844ad69...\"},{\"status\":201,\"eventId\":\"023972fe516f4ea7b2f722...\"}]"
{% endhighlight %}

So the error message speaks clearly for what's going wrong here: the JSON response here is an array of JSON objects, and JsonConvert can only serialize a single JSON object. Since using batch we're importing a large number of data at the same time, PredictionIO returns a list, not a single JSON object as in importing data line by line.

The solution I came up with here was relatively simple: just use the array as value, and append some name (such as 'importResponse') before the value, so that a JSON object is formed.

Note that the status in the JSON response is an extra information for the status of each piece of data in the batch, and it does not exist in normal import whose status can be directly observed from each single request.
