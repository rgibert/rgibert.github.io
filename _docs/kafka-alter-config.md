---
title: Change Kafka Topic Configuration
tags:
    - kafka
    - topics
---

# Change Kafka Topic Configuration

~~~ bash
kafka-configs \
    --alter \
    --entity-name ${topic} \
    --entity-type topics \
    --add-config key1=value1,key2=value2 \
    --zookeeper ${zookeeper_hosts}
~~~
