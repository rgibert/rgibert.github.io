---
title: OS
---

# Linux

## GZip

### Compress a File Without Removing It
~~~ bash
gzip < file > file.gz
~~~

## Systemd

### Setting OS Limits with systemd
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

## Command Line Tricks

### Recursively Set +x for Only Directories
Set the executable bit for directories (and not files) using +X (upper case) instead of +x (lower case).
~~~ bash
chmod g+rX *
~~~

### Prevent sudo Password Prompts

If you don't have NOPASSWD set in sudoers, you can still bypass the password prompt by setting SUDO_ASKPASS to a binary that echos your password.
~~~ bash
echo "echo mypassword" > ~/.local/bin/sudopass.sh
chmod 755 ~/.local/bin/sudopass.sh
export SUDO_ASKPASS=${HOME}/.local/bin/sudopass.sh
~~~

## SELinux

### Set Context for Container to Access Path

~~~ bash
semanage fcontext -a -t container_file_t '<path_root>(/.*)?'
restorecon -R <path_root>
~~~


# macOS

## Locking macOS Dock Content

~~~
defaults write com.apple.Dock position-immutable -bool yes; killall Dock
~~~

## Locking macOS Dock Size

~~~
defaults write com.apple.Dock size-immutable -bool yes; killall Dock
~~~

## Prevent sudo Password Prompts

See [Linux - Prevent sudo Password Prompts](https://richard.gibert.ca/linux#prevent-sudo-password-prompts)

## Disabling auto-hide scroll bars

System Preferences -> General -> Show scroll bars = Always