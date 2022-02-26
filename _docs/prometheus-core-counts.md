---
title: Prometheus Query Core/Thread Counts
tags:
    - code
    - prometheus
    - observability
    - monitoring
---

# Prometheus Query Core/Thread Counts

~~~ sql
count without(cpu, mode) (node_cpu_seconds_total{mode="idle"})
~~~
