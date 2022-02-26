---
title: Add Trusted Certificate Authority (CA) on macOS
tags:
    - macos
    - security
    - pem
    - tls
    - ssl
---

# Add Trusted Certificate Authority (CA) on macOS

~~~ bash
security add-trusted-cert -d -r trustRoot -k ~/Library/Keychains/login.keychain-db <CA_CERTIFICATE>
~~~
