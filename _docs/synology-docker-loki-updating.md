---
title: Synology - Updating Docker Loki Driver
tags:
    - synology
    - monitoring
    - observability
    - logging
    - loki
---

# Updating Docker Loki Driver
~~~ bash
docker plugin disable loki --force
docker plugin upgrade loki grafana/loki-docker-driver:latest --grant-all-permissions
docker plugin enable loki
synoservice --restart pkgctl-Docker
~~~
