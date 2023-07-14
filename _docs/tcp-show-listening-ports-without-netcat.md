---
title: Show listening TCP ports without netstat
tags:
    - network
    - tcp
---

# Show listening TCP ports without netstat

~~~ bash
declare -a ports=($(tail -n +2 /proc/net/tcp | cut -d":" -f"3" | cut -d" " -f"1"))
for port in ${ports[@]}; do
    echo $((0x${port}))
done | sort | uniq
~~~
