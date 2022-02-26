---
title: Get MegaRAID Enclosure ID
tags:
    - os
    - linux
    - raid
---

# Get MegaRAID Enclosure ID

~~~ bash
e=$(/opt/MegaRAID/MegaCli/MegaCli64 pdlist -a0 | grep Enc | grep -v 252 | awk ‘{print $4}' | sort | uniq  -c | awk ‘{print $2}')
~~~
