---
title: Consume Kafka messages with headers
tags:
    - kafka
---

# Consume Kafka messages with headers

Requires [kcat](https://github.com/edenhill/kcat) be installed.

~~~ bash
kcat \
    -e \
    -J \
    -F ${config_file} \
    -t ${topic} \
    -o ${start_offset} \
    -c ${number_of_offsets_to_consume}
~~~
