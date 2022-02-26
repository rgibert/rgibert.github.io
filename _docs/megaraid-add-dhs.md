---
title: Add Dynamic Hot Spare to Disk Group(s) in MegaRAID
tags:
    - os
    - linux
    - raid
---

# Add Dynamic Hot Spare to Disk Group(s) in MegaRAID

## Get MegaRAID Enclosure ID

See [Get MegaRAID Enclosure ID](megaraid-get-enclosure-id)

## Add Hostspare

~~~ bash
/opt/MegaRAID/storcli/storcli64 /c0/e${e}/s${slot} add hotsparedrive dgs=DG0[,DG1]
~~~
