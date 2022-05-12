---
title: Kubernetes list all images in pods
tags:
    - kubernetes
    - k8s
    - containers
---

# Kubernetes list all images in pods

~~~ bash
kubectl \
    get \
    pods \
    --all-namespaces \
    -o jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.containers[*]}{.image}{", "}{end}{end}' | \
    sort
~~~
