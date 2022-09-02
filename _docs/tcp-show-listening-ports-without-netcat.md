---
title: Show listening TCP ports without netcat
tags:
    - network
    - tcp
---

# Show listening TCP ports without netcat

~~~ bash
declare -a ports=($(tail -n +2 /proc/net/tcp | cut -d":" -f"3" | cut -d" " -f"1"))
for port in ${ports[@]}; do
    echo $((0x${port}))
done | sort | uniq
~~~
