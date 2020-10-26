---
title: Code
---

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
