---
title: Synology - Setup Unprivileged User Docker Access
tags:
    - synology
    - docker
    - containers
---

# Synology - Setup Unprivileged User Docker Access

1. Add your user to the docker group:
~~~ bash
synogroup --add docker <your_username>
~~~
1. Fix permissions on the Docker socket:
~~~ bash
chown root:docker /var/run/docker.sock
~~~
