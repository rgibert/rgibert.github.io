---
title: git push to multiple repositories
modified: 2020-03-26
tags: [git]
layout: post
---

Git can be configured to push a single remote to multiple URLs

{% highlight bash %}
git clone git@git...:... example
cd example
git remote set-url --add origin git@git2...:..
{% endhighlight %}

Now a git push from example will push to both the git and git2 repositories in parallel.
