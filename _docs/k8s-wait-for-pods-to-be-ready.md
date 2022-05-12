---
title: Wait for specific pods to be ready
tags:
    - kubernetes
    - k8s
    - containers
---

# Wait for specific pods to be ready

~~~ bash
kubectl \
    wait \
    --for=condition=ready \
    pod \
    -l \
    key1=value1
~~~
