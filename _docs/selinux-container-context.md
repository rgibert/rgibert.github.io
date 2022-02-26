---
title: Set SELinux Context for Container to Access Path
tags:
    - security
    - os
    - linux
    - containers
---

# Set SELinux Context for Container to Access Path

~~~ bash
semanage fcontext -a -t container_file_t '<path_root>(/.*)?'
restorecon -R <path_root>
~~~
