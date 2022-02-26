---
title: Setup Git GPG Signing
tags:
    - code
    - git
    - gpg
    - cryptography
---

# Setup Git GPG Signing

~~~ bash
git config --global gpg.program gpg
git config --global commit.gpgsign true
git config --global user.signingkey KEY_ID
~~~
