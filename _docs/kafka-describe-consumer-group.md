---
title: Show Kafka Consumer Group Details
tags:
    - kafka
    - consumer-groups
---

# Change Kafka Topic Configuration

~~~ bash
kafka-consumer-groups \
    --bootstrap-server ${kafka_hosts} \
    --describe \
    --group ${consumer_group}
~~~
