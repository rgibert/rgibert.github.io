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
