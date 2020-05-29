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

## Setup Unprivileged Docker Access

1. Add your user to the docker group:
~~~
synogroup --add docker <your_username>
~~~
1. Fix permissions on the Docker socket:
~~~
chown root:docker /var/run/docker.sock
~~~
