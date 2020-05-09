---
title: gzip Compressing Without Removing Original File
modified: 2020-05-08
tags: [docker, containers, heroku]
layout: post
---

Use the following to compress a file without removing the uncompressed file
{% highlight bash %}
gzip < file > file.gz
{% endhighlight %}
