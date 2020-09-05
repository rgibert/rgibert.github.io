---
title: Identity
---

# LDAP

## Generating Passwords for Principals

~~~ python
#!/usr/bin/env python
import base64
base64.b64encode(u'"PASSWORD"'.encode('UTF-16LE'))
~~~

## Creating Service Principals

1. Create LDIF:
~~~
dn: CN=PRINCIPAL_NAME,OU=OU0,DC=DC2,DC=DC1,DC=DC0
distinguishedName: CN=PRINCIPAL_NAME,OU=OU0,DC=DC2,DC=DC1,DC=DC0
objectClass: top
objectClass: person
objectClass: organizationPerson
objectClass: user
cn: PRINCIPAL_NAME
userPrincipalName: PRINCIPAL_NAME@REALM
servicePrincipalName: PRINCIPAL_NAME
unicodePwd:: BASE64_ENCODED_PRINCIPAL_PASSWORD
accountExpires: 0
userAccountControl: 66048
~~~

2. Apply LDIF:
~~~ bash
ldapadd -Z -D BIND_USER@REALM -h HOST -p PORT -W -f LDIF.ldif
~~~

## Updating Principal Passwords

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
