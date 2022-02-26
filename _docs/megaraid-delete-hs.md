---
title: Delete Hot Spare in MegaRAID
tags:
    - os
    - linux
    - raid
---

# Delete Hot Spare in MegaRAID

## Get MegaRAID Enclosure ID

See [Get MegaRAID Enclosure ID](megaraid-get-enclosure-id)

~~~ bash
/opt/MegaRAID/storcli/storcli64 /c0/e${e}/s${slot} delete hotsparedrive
~~~
