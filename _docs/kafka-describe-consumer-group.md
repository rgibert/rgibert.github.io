---
title: Show Kafka Consumer Group Details
tags:
    - kafka
    - consumer-groups
---

# Show Kafka Consumer Group Details

~~~ bash
kafka-consumer-groups \
    --bootstrap-server ${kafka_hosts} \
    --describe \
    --group ${consumer_group}
~~~
