---
title: Auto-Accept and Ignore Changes to SSH Host Keys
tags:
    - macos
    - linux
    - ssh
    - cryptography
---

# Auto-Accept and Ignore Changes to SSH Host Keys

NOTE: Security best practice is to validate host keys, this bypasses that.

Add the following to your ~/.ssh/config:
~~~
Host *
    GlobalKnownHostsFile /dev/null
    StrictHostKeyChecking no
~~~
