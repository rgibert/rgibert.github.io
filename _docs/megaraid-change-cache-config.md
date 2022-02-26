---
title: Change Cache Config in MegaRAID
tags:
    - os
    - linux
    - raid
---

# Change Cache Config in MegaRAID

~~~ bash
/opt/MegaRAID/MegaCli/MegaCli64 -LDSetProp WB -L${virtual_drive_num} -a0
/opt/MegaRAID/MegaCli/MegaCli64 -LDSetProp RA -L${virtual_drive_num} -a0
~~~
