---
title: Add Default SSH Key Passphrase to macOS Keychain
tags:
    - macos
    - ssh
    - cryptography
---

# Add Default SSH Key Passphrase to macOS Keychain

Add the following to your ~/.ssh/config:

~~~
Host *
    AddKeysToAgent yes
    UseKeychain yes
    ForwardAgent yes
~~~
