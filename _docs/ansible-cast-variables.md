---
title: Ansible - Always cast non-string variables
tags:
    - code
    - ansible
---

# Ansible - Always cast non-string variables

See [https://moreati.org.uk/blog/2020/07/05/ansible-is-stringly-typed.html](https://moreati.org.uk/blog/2020/07/05/ansible-is-stringly-typed.html)

~~~ yaml
when: (skip_install is not defined) or (not skip_install | bool)
~~~
