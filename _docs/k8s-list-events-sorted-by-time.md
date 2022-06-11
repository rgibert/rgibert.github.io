---
title: List all events sorted by lastTimestamp
tags:
    - kubernetes
    - k8s
    - containers
    - logs
---

# List all events sorted by lastTimestamp

~~~ bash
kubectl \
    get \
    events \
    --sort-by=".lastTimestamp"
~~~

# Filter for a specific pod sorted by lastTimestamp
~~~ bash
kubectl \
    get \
    events \
    --sort-by=".lastTimestamp" \
    --field-selector involvedObject.name=POD_NAME
~~~

# Exclude `Normal` events
~~~ bash
kubectl \
    get \
    events \
    --sort-by=".lastTimestamp" \
    --field-selector type!=Normal
~~~

# Grouping `--field-selector`
~~~ bash
kubectl \
    get \
    events \
    --sort-by=".lastTimestamp" \
    --field-selector involvedObject.name=POD_NAME,type!=Normal
~~~
