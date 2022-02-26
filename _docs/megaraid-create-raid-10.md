---
title: Create RAID-10 in MegaRAID
tags:
    - os
    - linux
    - raid
---

# Create RAID-10 in MegaRAID

## Get MegaRAID Enclosure ID

See [Get MegaRAID Enclosure ID](megaraid-get-enclosure-id)

## Create Array

~~~ bash
/opt/MegaRAID/MegaCli/MegaCli64 \
    -CfgSpanAdd \
    -r10 \
    -Array0[${e}:SLOT0,${e}:SLOT1] \
    -Array1[${e}:SLOT2,${e}:SLOT3] \
    wb ra nocachedbadbbu strpsz1024 -a
~~~
