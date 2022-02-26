---
title: Certificate Best Practices
tags:
    - ssl
    - tls
    - cryptography
    - security
    - jks
    - pkcs12
    - pem
---

# Certificate Best Practices

- Try to set certificates to expire during business hours on a work day.
- Don't use Java JKSes, they're deprecated and insecure, use PKCS#12 instead.
