---
title: Show Kafka Topic config
tags:
    - kafka
---

# Show Kafka Topic config

~~~ bash
kafka-topics \
    --zookeeper ${zookeeper_hosts} \
    --topic ${topic} \
    --describe
~~~
