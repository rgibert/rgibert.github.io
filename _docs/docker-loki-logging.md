---
title: Ship Docker Logs to Loki
tags:
    - docker
    - containers
    - observability
    - logging
    - loki
---

# Ship Docker Logs to Loki

1. Install the Loki driver plugin
~~~ bash
docker plugin \
    install \
    grafana/loki-docker-driver:latest \
    --alias loki \
    --grant-all-permissions
~~~

2. Change logger per container
~~~ bash
docker run \
    --log-driver=loki \
    --log-opt loki-url="LOKI_URL/loki/api/v1/push" \
    IMAGE
~~~
