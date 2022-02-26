---
title: Generating Base64 Encoded Strings
tags:
    - python
---

# Generating Base64 Encoded Strings

~~~ python
#!/usr/bin/env python
import base64
base64.b64encode(u'"PASSWORD"'.encode('UTF-16LE'))
~~~
