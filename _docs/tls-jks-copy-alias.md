---
title: JKS - Copy existing alias to a new alias
tags:
    - ssl
    - tls
    - cryptography
    - security
    - jks
    - pkcs12
    - keytool
---

# JKS - Copy existing alias to a new alias

~~~ bash
keytool \
    -keyclone \
    -keystore keystore.jks \
    -alias 'existing_alias' \
    -dest 'new_alias' \
    -keypass 'existing_key_password' \
    -newkeypass 'new_key_password'
~~~
