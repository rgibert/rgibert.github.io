---
title: Show CMD-TAB App Switcher on All Monitors on macOS
tags:
    - macos
---

# Show CMD-TAB App Switcher on All Monitors on macOS

~~~ bash
defaults write com.apple.Dock appswitcher-all-displays -bool true; killall Dock
~~~
