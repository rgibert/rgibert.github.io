---
title: Enable side-by-side diff for larger terms
tags:
    - delta
    - git
    - diff
    - shell
---

# Enable side-by-side diff for larger terms

Add the following to your `.zshrc` or `.bashrc`.

~~~ bash
export DELTA_FEATURES
function delta_sidebyside {
    if [[ "${COLUMNS} -ge 120 ]]; then
        DELTA_FEATURES="side-by-side"
    else
        DELTA_FEATURES=""
    fi
}
trap delta_sidebyside WINCH
~~~
