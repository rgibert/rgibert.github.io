---
title: Delete Virtual Drive in MegaRAID
tags:
    - os
    - linux
    - raid
---

# Delete Virtual Drive in MegaRAID

## Get MegaRAID Enclosure ID

See [Get MegaRAID Enclosure ID](megaraid-get-enclosure-id)

## Delete Vritual Drive

~~~ bash
/opt/MegaRAID/storcli/storcli64 /c0/v${virtual_drive_num} delete
~~~
