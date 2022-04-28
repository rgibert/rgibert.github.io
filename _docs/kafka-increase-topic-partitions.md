---
title: Increasing Partitions For a Kafka Topic
tags:
    - kafka
---

# Increasing Partitions For a Kafka Topic

1. Stop existing consumers.
2. Add paritions:
~~~ bash
kafka-topics \
    --zookeeper ${zookeeper_hosts} \
    --alter \
    --topic ${topic} \
    --paritions ${new_partition_count}
~~~
3. Check the reset of the offsets for the new paritions:
~~~ bash
kafka-consumer-groups \
    --bootstrap-server ${zookeeper_hosts} \
    --group ${consumer_group} \
    --topic ${topic}[:${new_parition_numbers_separated_by_commas}] \
    --reset-offsets \
    --to-earliest
~~~
4. Reset the offsets for the new paritions:
~~~ bash
kafka-consumer-groups \
    --bootstrap-server ${zookeeper_hosts} \
    --group ${consumer_group} \
    --topic ${topic}[:${new_parition_numbers_separated_by_commas}] \
    --reset-offsets \
    --to-earliest \
    --execute
~~~
5. Restart the consumers.