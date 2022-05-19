---
title: Grep through entire git history
tags:
    - code
    - git
    - search
---

# Grep through entire git history

~~~ bash
git rev-list --all | \
    xargs \
        git \
        grep \
        ${search_regex}
~~~
