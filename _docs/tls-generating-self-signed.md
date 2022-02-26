---
title: Generating a Self-Signed Certificate
tags:
    - ssl
    - tls
    - cryptography
    - security
    - pem
    - openssl
---

# Generating a Self-Signed Certificate

~~~ bash
openssl \
  req \
    -nodes \
    -x509 \
    -newkey rsa:4096 \
    -keyout key.pem \
    -out certificate.pem \
    -days 365 \
    -subj "/C=COUNTRY/ST=STATE/L=CITY/O=COMPANY/OU=ORG/CN=FQDN"
~~~
