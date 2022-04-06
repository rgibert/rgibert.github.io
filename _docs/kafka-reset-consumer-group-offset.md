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
    --group ${consumer_group} \
    --topic ${topic} \
    --reset-offsets \
    --to-latest \
    --execute
~~~

Available reset options:
~~~ bash
    --shift-by <integer> (note: can be negative)
    --to-current
    --to-latest
    --to-offset <offset_integer>
    --to-datetime <datetime_string>
    --by-duration <duration_string>
~~~
