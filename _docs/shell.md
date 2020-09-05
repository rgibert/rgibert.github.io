---
title: Shell
---

# Bash

## Force Command Prompt on New Line

From [https://www.vidarholen.net/contents/blog/?p=878](https://www.vidarholen.net/contents/blog/?p=878).

Some commands don't properly end their output with \n so your command prompt will be on the middle of the last line of their output.  This can be fixed using the following setting.

~~~ bash
PROMPT_COMMAND='printf "%%%$((COLUMNS-1))s\\r"'
~~~

## Loop Over Unique Pairings of Items
~~~ bash
set -- item0 item1 item2
for outer; do
    shift
    for inner; do
        echo "${outer}-${inner}"
    done
done
~~~

# Zsh

## Suffix Aliases

Suffix aliases will match file suffixes.    

The following opens vscode when you enter any .md filename:
~~~ bash
alias -s md=code
~~~

The following will run git clone for any .git repository pasted into the command line:
~~~ bash
alias -s git="git clone"
~~~

## Global Aliases

Matches all usage in a line, example:
~~~ bash
alias -g G="| grep "
ps ux G foo
~~~
