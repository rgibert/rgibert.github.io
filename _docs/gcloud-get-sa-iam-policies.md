---
title: Get All IAM Policies For a GCP Service Account
tags:
    - cloud
    - gcp
    - iam
    - service-accounts
    - permissions
---

# Get All IAM Policies For a GCP Service Account

~~~ bash
gcloud \
    projects \
    get-iam-policy \
    ${project_name} \
    --flatten="bindings[].members" \
    --format="table(bindings.roles)" \
    --filter="bindings.members:${service_account}"
~~~
