---
title: Kubernetes List all Images in Pods
tags:
    - kubernetes
    - k8s
    - containers
---

# Kubernetes List all Images in Pods

~~~ bash
kubectl \
    get \
    pods \
    --all-namespaces \
    -o jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.containers[*]}{.image}{", "}{end}{end}' | \
    sort
~~~
