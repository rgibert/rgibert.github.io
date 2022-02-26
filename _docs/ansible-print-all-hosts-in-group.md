---
title: Ansible - Print all hosts in a group
tags:
    - code
    - ansible
---

# Ansible - Print all hosts in a group

~~~ bash
ansible localhost -i <inventory> -m debug -a "var=groups['<group_name>']"
~~~
