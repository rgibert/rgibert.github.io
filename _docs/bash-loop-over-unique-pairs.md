---
title: Loop Over Unique Pairings of Items in Bash
tags:
    - code
    - bash
    - shell
---

# Loop Over Unique Pairings of Items in Bash
~~~ bash
set -- item0 item1 item2
for outer; do
    shift
    for inner; do
        echo "${outer}-${inner}"
    done
done
~~~
