---
title: Print all certificates in a bundle
tags:
    - ssl
    - tls
    - cryptography
    - security
    - pem
    - keytool
---

# Print all certificates in a bundle

~~~ bash
keytool -printcert -v -file bundle.pem | grep Owner
~~~
