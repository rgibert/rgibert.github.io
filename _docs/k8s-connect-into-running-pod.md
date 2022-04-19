---
title: Get a shell in a running Kubernetes pod
tags:
    - kubernetes
    - k8s
    - containers
---

# Kubernetes List all Images in Pods

~~~ bash
kubectl \
    exec \
    --stdin \
    --tty \
    ${pod_name} \
    -- \
    /bin/sh
~~~
