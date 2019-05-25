---
title: Looping over unique items in bash
modified: 2018-03-03
tags: [bash]
layout: post
---

The following is useful when you have a list of items and you need to loop through all the unique pairings:

{% highlight bash %}
set -- item0 item1 item2
for outer; do
    shift
    for inner; do
        echo "${outer}-${inner}"
    done
done
{% endhighlight %}
