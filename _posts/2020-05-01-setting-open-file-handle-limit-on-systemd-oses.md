---
title: Setting open file handle limit on systemd OSes
modified: 2020-05-01
tags: [linux, systemd]
layout: post
---

Systemd enforces system limits outside /etc/security/limits.conf so the following changes are required to set nofile on systemd hosts.

1. Edit /etc/systemd/user.conf and /etc/systemd/systemd.conf, add the following line to each file:

{% highlight bash %}
DefaultLimitNOFILE=NEW_LIMIT
{% endhighlight %}

2. Edit /etc/security/limits.conf and set the usual limit details:
{% highlight bash %}
USER soft nofile NEW_LIMIT
USER hard nofile NEW_LIMIT
{% endhighlight %}

3. Restart your system for the changes to take effect.
