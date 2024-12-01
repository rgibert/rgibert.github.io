---
title: GitHub get main/master branch SHA
tags:
    - code
    - git
    - github
---

# GitHub get main/master branch SHA

~~~ bash
gh api repos/${org}/${repository}/commits/main --jq “.sha”
~~~
