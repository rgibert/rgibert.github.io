---
title: Zsh Suffix Aliases
tags:
    - code
    - zsh
    - shell
---

# Zsh Suffix Aliases

Suffix aliases will match file suffixes.    

The following opens vscode when you enter any .md filename:
~~~ bash
alias -s md=code
~~~

The following will run git clone for any .git repository pasted into the command line:
~~~ bash
alias -s git="git clone"
~~~
