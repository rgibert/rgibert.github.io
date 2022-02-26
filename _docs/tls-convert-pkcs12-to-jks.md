---
title: Convert PKCS#12 to JKS
tags:
    - ssl
    - tls
    - cryptography
    - security
    - jks
    - pkcs12
    - keytool
---

# Convert PKCS#12 to JKS

NOTE: JKS is deprecated, you should use PKCS#12 instead.

~~~ bash
keytool \
  -importkeystore \
  -srckeystore input.pkcs12 \
  -srcstoretype PKCS12 \
  -destkeystore output.jks \
  -deststoretype JKS
~~~
