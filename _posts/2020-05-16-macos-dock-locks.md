---
title: Locking the macOS Dock
modified: 2020-05-16
tags: [macos]
layout: post
---

To lock the content of macOS's dock:
{% highlight bash %}
defaults write com.apple.Dock position-immutable -bool yes; killall Dock
{% endhighlight %}

To lock the size of macOS's dock:
{% highlight bash %}
defaults write com.apple.Dock size-immutable -bool yes; killall Dock
{% endhighlight %}
