---
title: Limit Git Clone to Just Master Branch For Performance
tags:
    - code
    - git
---

# Limit Git Clone to Just Master Branch For Performance

When cloning large repositories with many branches, you can isolate the branch you'd like to clone (good for builds) but setting the fetch refspec as follows:

~~~ bash
git clone -c remote.origin.fetch=+refs/heads/master:refs/remotes/origin/master repo
~~~
