---
title: Using `uv` to self-manage dependencies
tags:
    - python
    - uv
---

# Using `uv` to self-manage dependencies

If you have a standalone Python script which has dependencies, rather than fighting having to setup virtual environments and managing dependencies before running you can use `uv` in the scritps shebang to handle dependencies in a virtual environment for you by setting the following a the start of your script:

~~~ python
#!/usr/bin/env -S uv run --script
# /// script
# requires-python = ">=3.12"
# dependencies = [
#     "click",
#     "rich",
# ]
# ///
~~~

This tells the script to use at least Python 3.12 and to install `click` and `rich` dependencies before starting.

`uv` will try to find and re-use the virtual environment on re-runs.