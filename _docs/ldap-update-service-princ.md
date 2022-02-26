---
title: Updating LDAP Service Principal Passwords
tags:
    - identity
    - ldap
    - authentication
---

# Generate a Base64 Encoded Password

See [Generating Base64 Encoded Strings](python-gen-base64-string)

# Update Service Principal Passwords

1. Create LDIF:
~~~
dn: CN=PRINCIPAL_NAME,OU=OU0,DC=DC2,DC=DC1,DC=DC0
changetype: modify
replace: unicodePwd
unicodePwd:: BASE64_ENCODED_PRINCIPAL_PASSWORD
~~~

2. Apply LDIF:
~~~ bash
ldapmodify -Z -D BIND_USER@REALM -h HOST -p PORT -W -f LDIF.ldif
~~~
