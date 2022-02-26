---
title: Dump endpoint certificate to a PEM file
tags:
    - ssl
    - tls
    - cryptography
    - security
    - pem
    - openssl
---

# Dump endpoint certificate to a PEM file

~~~ bash
openssl \
    s_client \
    -showcerts \
    -connect HOST:PORT \
    </dev/null \
    2>/dev/null \
    | openssl x509 \
        -outform PEM
~~~
