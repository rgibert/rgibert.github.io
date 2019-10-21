---
title: Montioring Synology's Docker Daemon with Prometheus
modified: 2019-10-20
tags: [monitoring,docker,containers,prometheus]
layout: post
---

Docker can be configured to expose Prometheus formated metrics, to enable this functionality you need to add the
following to /var/packages/Docker/etc/dockerd.json :

{% highligh json %}
{
  "experimental" : true,
  "metrics-addr" : "0.0.0.0:9999",
}
{% endhighlight %}

Once updated, restart your Docker package for the changes to take effect.
