---
title: Disable Touchpad Swipe Back on macOS
tags:
    - macos
    - browsers
    - firefox
    - chrome
    - brave
    - safari
---

# Disable Touchpad Swipe Back on macOS

~~~ bash
# Chrome
defaults write com.google.Chrome AppleEnableSwipeNavigateWithScrolls -bool FALSE
# FireFox
defaults write org.mozilla.firefox AppleEnableSwipeNavigateWithScrolls -bool FALSE
# Brave
defaults write com.brave.Browser AppleEnableSwipeNavigateWithScrolls -bool FALSE
# Safari
defaults write com.apple.Safari AppleEnableSwipeNavigateWithScrolls -bool FALSE
~~~
