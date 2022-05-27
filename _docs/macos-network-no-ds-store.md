---
title: Don't create .DS_Store files on network/removable volumes
tags:
    - macos
---

# Don't create .DS_Store files on network/removable volumes

~~~ bash
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool true
defaults write com.apple.desktopservices DSDontWriteUSBStores -bool true
~~~
