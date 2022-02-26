---
title: Generating a Key and Certificate Signing Request (CSR)
tags:
    - ssl
    - tls
    - cryptography
    - security
    - pem
    - csr
    - openssl
---

# Generating a Key and Certificate Signing Request (CSR)

~~~ bash
openssl \
    -out fqdn.csr \
    -new \
    -newkey rsa:4096 \
    -nodes \
    -keyout fqdn.key \
    -subj "/C=COUNTRY/ST=STATE/L=CITY/O=COMPANY/OU=ORG/CN=FQDN"
~~~
