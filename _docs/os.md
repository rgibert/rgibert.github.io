---
title: OS
---

# Linux

## FFMPEG

### Speed up audio of a file

NOTE: ACCELERATION can be a value from "0.5" (1/2 speed) to "2.0" (double speed)

~~~ bash
ffmpeg -i INPUT_FILE -filter:a "atempo=ACCELERATION" -vn OUTPUT_FILE
~~~

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

## MegaRAID

## Get Enclosure ID

~~~
e=$(/opt/MegaRAID/MegaCli/MegaCli64 pdlist -a0 | grep Enc | grep -v 252 | awk ‘{print $4}' | sort | uniq  -c | awk ‘{print $2}')
~~~

## Create RAID-1
~~~
/opt/MegaRAID/MegaCli/MegaCli64 \
    -CfgLdAdd \
    -r1 \
    [${e}:SLOT0,${e}:SLOT1] \
    wb ra nocachedbadbbu strpsz1024 -a
~~~

## Create RAID-10

~~~
/opt/MegaRAID/MegaCli/MegaCli64 \
    -CfgSpanAdd \
    -r10 \
    -Array0[${e}:SLOT0,${e}:SLOT1] \
    -Array1[${e}:SLOT2,${e}:SLOT3] \
    wb ra nocachedbadbbu strpsz1024 -a
~~~

## Add Dynamic Hot Spare to Disk Group(s)

~~~
/opt/MegaRAID/storcli/storcli64 /c0/e${e}/s${slot} add hotsparedrive dgs=DG0[,DG1]
~~~

## Delete JBODs

~~~
/opt/MegaRAID/storcli/storcli64 /c0/e${e}/s${slot} set good force
~~~

## Delete Virtual Drive

~~~
/opt/MegaRAID/storcli/storcli64 /c0/v${virtual_drive_num} delete
~~~

## Delete Hot Spare

~~~
/opt/MegaRAID/storcli/storcli64 /c0/e${e}/s${slot} delete hotsparedrive
~~~

## Show Critical Events

~~~
/opt/MegaRAID/storcli/storcli64 /c0 show events filter=critical
~~~

## Change Cache Config

~~~
/opt/MegaRAID/MegaCli/MegaCli64 -LDSetProp WB -L${virtual_drive_num} -a0
/opt/MegaRAID/MegaCli/MegaCli64 -LDSetProp RA -L${virtual_drive_num} -a0
~~~

# GPG

## Generate New Key

~~~
gpg --full-generate-key
~~~

## List Keys

~~~
gpg --list-secret-keys --keyid-format LONG
~~~

## Export Key

~~~
gpg --armor --export KEY_ID
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

## Show CMD-TAB App Switcher On All Monitors
~~~
defaults write com.apple.Dock appswitcher-all-displays -bool true; killall Dock
~~~

## Prevent sudo Password Prompts

See [Linux - Prevent sudo Password Prompts](os#prevent-sudo-password-prompts)

## Disabling auto-hide scroll bars

System Preferences -> General -> Show scroll bars = Always

## Disable Touchpad Swipe Back

~~~
# Chrome
defaults write com.google.Chrome AppleEnableSwipeNavigateWithScrolls -bool FALSE
# FireFox
defaults write org.mozilla.firefox AppleEnableSwipeNavigateWithScrolls -bool FALSE
# Brave
defaults write com.brave.Browser AppleEnableSwipeNavigateWithScrolls -bool FALSE
# Safari
defaults write com.apple.Safari AppleEnableSwipeNavigateWithScrolls -bool FALSE
~~~

## Disable Dock Bouncing Icons

~~~
defaults write com.apple.dock no-bouncing -bool TRUE; killall Dock
~~~
