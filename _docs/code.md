---
title: Code
---

# Android

## Wireless ADB

- Install [Android Platform Tools](https://developer.android.com/studio/releases/platform-tools).
- Enable Developer tools on the Android device.
- Enable "Wireless Debugging" on the Android device.
- Pair ADB
~~~ bash
adb pair host:port
~~~
- Connect ADB
~~~ bash
adb connect host:port
~~~

# Ansible

## Always cast non-string variables

See [https://moreati.org.uk/blog/2020/07/05/ansible-is-stringly-typed.html](https://moreati.org.uk/blog/2020/07/05/ansible-is-stringly-typed.html)

~~~ yaml
when: (skip_install is not defined) or (not skip_install | bool)
~~~

## Print all hosts in a group

~~~ bash
ansible localhost -i <inventory> -m debug -a "var=groups['<group_name>']"
~~~

## Key/CSR Generation with Vaulting

~~~ bash
export F=FQDN
export TLS_BITS=4096
export C=Canada
export ST=Ontario
export L=Toronto
export O=Company
export OU=Dept
export EMAIL=email@company.com

# Generate new key and csr
openssl req \
    -out "host_files/${F}/${F}.csr" \
    -new \
    -newkey rsa:${TLS_BITS} \
    -nodes \
    -keyout "host_vars/${F}/vault_tls_private_key" \
    -subj "/C=${COUNTRY}/ST=${ST}/L=${L}/O=${O}/OU=${OU}/CN=${F}/emailAddress=${EMAIL}"

# indent the key file
sed -i 's/^/\ \ /g' "host_vars/${F}/vault_tls_private_key"

# add YAML header for Ansible variable
sed -i '1s/^/---\ntls_private_key: |\n/' "host_vars/${F}/vault_tls_private_key"

# vault the TLS private key
ansible-vault \
    encrypt \
    "host_vars/${F}/vault_tls_private_key"
~~~

# Docker

## Get CPU allocation

~~~ bash
cat /sys/fs/cgroup/cpuacct/cpu.cfs_quota_us
~~~

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

## Limit Clone to Just Master Branch For Performance

When cloning large repositories with many branches, you can isolate the branch you'd like to clone (good for builds) but setting the fetch refspec as follows:

~~~ bash
git clone -c remote.origin.fetch=+refs/heads/master:refs/remotes/origin/master repo
~~~

## Setup GPG Signing

~~~ bash
git config --global gpg.program gpg
git config --global commit.gpgsign true
git config --global user.signingkey KEY_ID
~~~

# HTML

## Small/Basic Favicons

From [https://news.ycombinator.com/item?id=24111105](https://news.ycombinator.com/item?id=24111105).

~~~ html
<link rel="icon" href="data:image/gif;base64,R0lGODlhEAAQAAAAACwAAAAAAQABAAACASgAOw==">
~~~

# Prometheus

## Query Core/Thread Counts

~~~ promql
count without(cpu, mode) (node_cpu_seconds_total{mode="idle"})
~~~

# Python

## Get Supported TLS Versions

~~~ python
python -c "import requests; print(requests.get('https://www.howsmyssl.com/a/check').json()['tls_version'])"
~~~

# Shell

## Bash

### Force Command Prompt on New Line

From [https://www.vidarholen.net/contents/blog/?p=878](https://www.vidarholen.net/contents/blog/?p=878).

Some commands don't properly end their output with \n so your command prompt will be on the middle of the last line of their output.  This can be fixed using the following setting.

~~~ bash
PROMPT_COMMAND='printf "%%%$((COLUMNS-1))s\\r"'
~~~

### Loop Over Unique Pairings of Items
~~~ bash
set -- item0 item1 item2
for outer; do
    shift
    for inner; do
        echo "${outer}-${inner}"
    done
done
~~~

## Zsh

### Suffix Aliases

Suffix aliases will match file suffixes.    

The following opens vscode when you enter any .md filename:
~~~ bash
alias -s md=code
~~~

The following will run git clone for any .git repository pasted into the command line:
~~~ bash
alias -s git="git clone"
~~~

### Global Aliases

Matches all usage in a line, example:
~~~ bash
alias -g G="| grep "
ps ux G foo
~~~

# Splunk

## Reverse Order Of Events

Append the following to the end of your query.
~~~
| reverse
~~~
