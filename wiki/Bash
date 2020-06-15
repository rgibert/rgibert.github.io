# Bash

## Force Command Prompt on New Line

From (https://www.vidarholen.net/contents/blog/?p=878)[https://www.vidarholen.net/contents/blog/?p=878].

Some commands don't properly end there output with \n so your command prompt will be on the middle of the last line of their output.  This can be fixed using the following setting.

~~~ bash
PROMPT_COMMAND='printf "%%%$((COLUMNS-1))s\\r"'
~~~
