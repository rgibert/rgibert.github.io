---
title: Create RAID-1 in MegaRAID
tags:
    - os
    - linux
    - raid
---

# Create RAID-1 in MegaRAID

## Get MegaRAID Enclosure ID

See [Get MegaRAID Enclosure ID](megaraid-get-enclosure-id)

## Create Array

~~~ bash
/opt/MegaRAID/MegaCli/MegaCli64 \
    -CfgLdAdd \
    -r1 \
    [${e}:SLOT0,${e}:SLOT1] \
    wb ra nocachedbadbbu strpsz1024 -a
~~~
