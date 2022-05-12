---
title: Watch all warnings
tags:
    - kubernetes
    - k8s
    - containers
---

# Watch all warnings

~~~ bash
kubectl \
    get \
    events \
    -w \
    --field-selector=type=Warning \
    -A
~~~
