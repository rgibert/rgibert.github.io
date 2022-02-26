---
title: Setting OS Limits with systemd
tags:
    - os
    - linux
    - systemd
---

# Setting OS Limits with systemd
1. Edit /etc/systemd/user.conf and /etc/systemd/systemd.conf, add the following line to each file:
~~~
DefaultLimitNOFILE=NEW_LIMIT
~~~
1. Edit /etc/security/limits.conf and set the usual limit details:
~~~
USER soft nofile NEW_LIMIT
USER hard nofile NEW_LIMIT
~~~
1. Restart your system for the changes to take effect.
