---
title: Disabling auto-hide scroll bars on macOS
tags:
    - macos
---

# Disabling auto-hide scroll bars on macOS

## UI

System Preferences -> General -> Show scroll bars = Always

## Shell

~~~ bash
defaults write NSGlobalDomain AppleShowScrollBars -string "Always"
~~~
