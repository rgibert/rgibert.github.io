---
title: Get the Earliest Kafka Partition Offsets Available
tags:
    - kafka
---

# Get the Earliest Kafka Partition Offsets Available

~~~ bash
kafka-run-class \
    kafka.tools.GetOffsetShell \
    --broker-list ${broker} \
    --topic ${topic} \
    --time -2
~~~
