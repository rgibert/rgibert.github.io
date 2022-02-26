---
title: Get Python's Supported TLS Versions
tags:
    - code
    - python
    - tls
    - ssl
    - cryptography
---

# Get Python's Supported TLS Versions

~~~ python
python -c "import requests; print(requests.get('https://www.howsmyssl.com/a/check').json()['tls_version'])"
~~~
