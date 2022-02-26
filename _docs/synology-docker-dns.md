---
title: Synology - Set Custom DNS Servers for Docker
tags:
    - synology
    - dns
    - docker
    - containers
---

# Synology - Set Custom DNS Servers for Docker
1. Edit /var/packages/Docker/etc/dockerd.json:
~~~ json
{
    "dns": ["SERVER_0", "SERVER_1"]
}
~~~

2. Restart the Docker package
~~~ bash
synoservice --restart pkgctl-Docker
~~~
