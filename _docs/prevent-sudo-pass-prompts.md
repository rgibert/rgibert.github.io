---
title: Prevent sudo Password Prompts
tags:
    - os
    - linux
    - macos
---

# Prevent sudo Password Prompts

If you don't have NOPASSWD set in sudoers, you can still bypass the password prompt by setting SUDO_ASKPASS to a binary that echos your password.
~~~ bash
echo "echo mypassword" > ~/.local/bin/sudopass.sh
chmod 755 ~/.local/bin/sudopass.sh
export SUDO_ASKPASS=${HOME}/.local/bin/sudopass.sh
~~~
