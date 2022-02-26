---
title: Print Certificate Expiry for an Endpoint
tags:
    - ssl
    - tls
    - cryptography
    - security
    - openssl
---

# Print Certificate Expiry for an Endpoint

~~~ bash
openssl \
    s_client \
    -connect HOST:PORT 2>/dev/null <<< "Q" \
    | openssl x509 -text \
    | grep "Not After :"
~~~
