---
title: Synology
---

## Enable Prometheus Formatted Metrics for Synology Docker

1. Edit /var/packages/Docker/etc/dockerd.json:
~~~ json
{
  "experimental" : true,
  "metrics-addr" : "0.0.0.0:9999",
}
~~~
1. Restart the Docker package
~~~ bash
synoservice --restart pkgctl-Docker
~~~

## Set Custom DNS Servers
1. Edit /var/packages/Docker/etc/dockerd.json:
~~~ json
{
  "dns": ["SERVER_0", "SERVER_1"]
}
~~~
1. Restart the Docker package

## Setup Unprivileged Docker Access

1. Add your user to the docker group:
~~~ bash
synogroup --add docker <your_username>
~~~
1. Fix permissions on the Docker socket:
~~~ bash
chown root:docker /var/run/docker.sock
~~~

## Ship Docker Logs to Loki

1. Install the Loki driver plugin
~~~ bash
docker plugin \
  install \
  grafana/loki-docker-driver:latest \
  --alias loki \
  --grant-all-permissions
~~~
1. Change logger per container
~~~ bash
docker run \
  --log-driver=loki \
  --log-opt loki-url="LOKI_URL/loki/api/v1/push" \
  IMAGE
~~~

## Updating Docker Loki Driver
~~~ bash
docker plugin disable loki --force
docker plugin upgrade loki grafana/loki-docker-driver:latest --grant-all-permissions
docker plugin enable loki
synoservice --restart pkgctl-Docker
~~~
