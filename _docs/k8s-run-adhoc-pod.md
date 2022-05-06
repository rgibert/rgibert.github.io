---
title: Run an ad-hoc pod in Kubernetes
tags:
    - kubernetes
    - k8s
    - containers
---

# Run an ad-hoc pod in Kubernetes

~~~ bash
kubectl \
    run \
    -i \
    -tty \
    --rm \
    ${pod_name} \
    --image=${container_image} \
    --restart=Never \
    -- \
    /bin/sh
~~~
