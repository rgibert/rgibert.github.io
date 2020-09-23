---
title: SSL/TLS
---

## Best Practices

- Try to set certificates to expire during business hours on a work day.
- Don't use Java JKSes, they're deprecated and insecure, use PKCS#12 instead.

# Utilities

## List an Endpoints's Supported Ciphers

~~~ bash
nmap \
    --script ssl-enum-ciphers \
    -Pn PORT HOST
~~~

## Print Certificate Expiry for an Endpoint

~~~ bash
openssl \
    s_client \
    -connect HOST:PORT 2>/dev/null <<< "Q" \
    | openssl x509 -text \
    | grep "Not After :"
~~~

# PEM

## Generating a Key and CSR

~~~ bash
openssl \
    -out fqdn.csr \
    -new \
    -newkey rsa:4096 \
    -nodes \
    -keyout fqdn.key \
    -subj "/C=COUNTRY/ST=STATE/L=CITY/O=COMPANY/OU=ORG/CN=FQDN"
~~~

## Generating a Self-Signed Certificate

~~~ bash
openssl \
  req \
    -nodes \
    -x509 \
    -newkey rsa:4096 \
    -keyout key.pem \
    -out certificate.pem \
    -days 365 \
    -subj "/C=COUNTRY/ST=STATE/L=CITY/O=COMPANY/OU=ORG/CN=FQDN"
~~~

## Verify Certificate and Key Match

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

## Print all certificates in a bundle

~~~ bash
keytool -printcert -v -file bundle.pem | grep Owner
~~~

## Dump endpoint certificate to a PEM file

~~~ bash
openssl \
    s_client \
    -showcerts \
    -connect HOST:PORT \
    </dev/null \
    2>/dev/null \
    | openssl x509 \
        -outform PEM
~~~


# PKCS#12

## Convert PEM to PKCS#12

~~~ bash
openssl \
  pkcs12 \
    -export \
    -out output.pkcs12 \
    -in certificate.pem \
    -inkey key.pem
~~~

# JKS

## Convert PKCS#12 to JKS

NOTE: JKS is deprecated, you should use PKCS#12 instead.

~~~ bash
keytool \
  -importkeystore \
  -srckeystore input.pkcs12 \
  -srcstoretype PKCS12 \
  -destkeystore output.jks \
  -deststoretype JKS
~~~

## Copy existing alias to a new alias

~~~ bash
keytool \
    -keyclone \
    -keystore keystore.jks \
    -alias 'existing_alias' \
    -dest 'new_alias' \
    -keypass 'existing_key_password' \
    -newkeypass 'new_key_password'
~~~
