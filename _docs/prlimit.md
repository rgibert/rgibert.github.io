---
title: Use prlimit to Increase Limits of a Running Process
tags:
    - os
    - linux
    - macos
    - limits
    - shell
---

# Use prlimit to Increase Limits of a Running Process

## Show limits

~~~ bash
prlimit \
    --pid ${pid}
~~~

## Increase `nproc`

~~~ bash
prlimit \
    --pid ${pid} \
    --nproc=${nproc_limit}
~~~