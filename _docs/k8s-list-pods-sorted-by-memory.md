---
title: Get a list of pods sorted by memory usage
tags:
    - kubernetes
    - k8s
    - containers
---

# Get a list of pods sorted by memory usage

~~~ bash
kubectl \
    top \
    pods \
    -A \
    --sort-by='memory'
~~~
