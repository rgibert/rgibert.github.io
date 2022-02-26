---
title: Creating Service Principals in LDAP
tags:
    - identity
    - ldap
    - authentication
---

# Generate a Base64 Encoded Password

See [Generating Base64 Encoded Strings](python-gen-base64-string)

# Create Service Principals in LDAP

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
