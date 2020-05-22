# Synology

## Enable Prometheus Formatted Metrics for Synology Docker

1. Edit /var/packages/Docker/etc/dockerd.json:
~~~
{
  "experimental" : true,
  "metrics-addr" : "0.0.0.0:9999",
}
~~~
1. Restart the Docker package
