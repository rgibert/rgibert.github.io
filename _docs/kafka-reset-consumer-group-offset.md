---
title: Reset Kafka Consumer Group Offset
tags:
    - kafka
    - consumer-groups
---

# Reset Kafka Consumer Group Offset

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

# Reset Kafka Consumer Group Offset for a Specific Partition

~~~ bash
kafka-consumer-groups \
    --bootstrap-server ${kafka_hosts} \
    --group ${consumer_group} \
    --topic ${topic}:${partition_number} \
    --reset-offsets \
    --to-latest \
    --execute
~~~
