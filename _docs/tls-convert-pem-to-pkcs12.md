---
title: Convert PEM to PKCS#12
tags:
    - ssl
    - tls
    - cryptography
    - security
    - pem
    - pkcs12
    - openssl
---

# Convert PEM to PKCS#12

~~~ bash
openssl \
  pkcs12 \
    -export \
    -out output.pkcs12 \
    -in certificate.pem \
    -inkey key.pem
~~~
