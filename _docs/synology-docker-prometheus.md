---
title: Synology - Enable Prometheus Formatted Metrics for Synology Docker
tags:
    - synology
    - monitoring
    - observability
    - monitoring
    - prometheus
    - docker
    - containers
---

# Synology - Enable Prometheus Formatted Metrics for Synology Docker

1. Edit /var/packages/Docker/etc/dockerd.json:
~~~ json
{
    "experimental" : true,
    "metrics-addr" : "0.0.0.0:9999",
}
~~~

2. Restart the Docker package
~~~ bash
synoservice --restart pkgctl-Docker
~~~
