---
title: Manually trigger a job from a cronjob
tags:
    - kubernetes
    - k8s
    - containers
    - cron
---

# Manually trigger a job from a cronjob

~~~ bash
kubectl \
    create \
    job \
    --from=cronjob/${cronjob_name} \
    ${manual_job_name}
~~~
