# Git

## Global Ignore File

~~~ bash
git config --global core.excludesfile ~/.config/git/gitignore
~~~

## Pushing to Multiple Repositories

~~~ bash
git clone repo1 example
cd example
git remote set-url --add origin repo2
~~~

## Multi-line Commit Messages From CLI

~~~ bash
git commit -m "line 1" -m "line 2"
~~~
