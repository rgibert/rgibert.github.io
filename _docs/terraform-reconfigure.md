---
title: Terraform init reporting bucket doesn't exist when it does
tags:
    - terraform
    - gcp
    - aws
    - azure
---

# `terraform init` reporting bucket doesn't exist when it does

If you see the following error when trying to run `terraform init`:

~~~
Error: Failed to get existing workspaces: querying Cloud Storage failed: bucket doesn't exist
~~~

Terraform may be confused, this can usually be fixed after fixing the bucket name with `terraform init -reconfigure`.
