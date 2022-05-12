---
title: Get a list of pods and the node they run on
tags:
    - kubernetes
    - k8s
    - containers
---

# Get a list of pods and the node they run on

~~~ bash
kubectl \
    get \
    po \
    -o=custom-columns=NODE:.spec.nodeName,NAME:.metadata.name
~~~
