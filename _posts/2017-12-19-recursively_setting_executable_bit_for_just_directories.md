---
title: Recursively setting executable bit for just directories
modified: 2017-12-19 16:13
tags: [linux]
layout: post
---

You can easily just set the executable bit for directories (and not files) using +X (upper case) instead of +x (lower case).

Example:

{% highlight bash %}
$ ls -l
total 8
drwx------ 2 richard richard 4096 Dec 19 19:48 dir0
drwx------ 2 richard richard 4096 Dec 19 19:48 dir1
-rw------- 1 richard richard    0 Dec 19 19:48 file0.txt
-rw------- 1 richard richard    0 Dec 19 19:48 file1.txt

$ chmod g+rX *

$ ls -l
total 8
drwxr-x--- 2 richard richard 4096 Dec 19 19:48 dir0
drwxr-x--- 2 richard richard 4096 Dec 19 19:48 dir1
-rw-r----- 1 richard richard    0 Dec 19 19:48 file0.txt
-rw-r----- 1 richard richard    0 Dec 19 19:48 file1.txt
{% endhighlight %}
