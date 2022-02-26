---
title: Verify Certificate and Key Match
tags:
    - ssl
    - tls
    - cryptography
    - security
    - pem
    - openssl
---

# Verify Certificate and Key Match

~~~ bash
export FQDN=DOMAIN_TO_VALIDATE
export C=$(openssl x509 -noout -modulus -in ${FQDN}.cer | openssl md5)
export K=$(openssl rsa -noout -modulus -in ${FQDN}.key | openssl md5)
if [[ $(diff <(echo ${C}) <(echo ${K}) | wc -l) -eq 0 ]]; then
    echo "Key pair match"
else
    echo "Key pair DO NOT match"
fi
~~~
