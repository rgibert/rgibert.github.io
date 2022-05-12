---
title: List a pod's events sorted by lastTimestamp
tags:
    - kubernetes
    - k8s
    - containers
    - logs
---

# List a pod's events sorted by lastTimestamp

~~~ bash
kubectl \
    get \
    events \
    --sort-by=".lastTimestamp"
~~~
