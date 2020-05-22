# macOS

## Locking macOS Dock Content

~~~
defaults write com.apple.Dock position-immutable -bool yes; killall Dock
~~~

## Locking macOS Dock Size

~~~
defaults write com.apple.Dock size-immutable -bool yes; killall Dock
~~~
