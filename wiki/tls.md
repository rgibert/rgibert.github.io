# SSL/TLS

## List an Endpoints's Supported Ciphers

~~~
nmap --script ssl-enum-ciphers -Pn PORT HOST
~~~

## Print Certificate Expiry for an Endpoint

~~~
openssl s_client -connect HOST:PORT 2>/dev/null <<< "Q" | openssl x509 -text | grep "Not After :"
~~~

## Generating a Self-Signed Certificate

~~~
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

## Convert PEM to PKCS#12

~~~
openssl \
  pkcs12 \
    -export \
    -out output.pkcs12 \
    -in certificate.pem \
    -inkey key.pem
~~~

## Convert PKCS#12 to JKS

NOTE: JKS is deprecated, you should use PKCS#12 instead.

~~~
keytool \
  -importkeystore \
  -srckeystore input.pkcs12 \
  -srcstoretype PKCS12 \
  -destkeystore output.jks \
  -deststoretype JKS
~~~

## Verify Certificate and Key Match

~~~
export FQDN=DOMAIN_TO_VALIDATE
export C=$(openssl x509 -noout -modulus -in ${FQDN}.cer | openssl md5)
export K=$(openssl rsa -noout -modulus -in ${FQDN}.key | openssl md5)
if [[ $(diff <(echo ${C}) <(echo ${K}) | wc -l) -eq 0 ]]; then
    echo "Key pair match"
else
    echo "Key pair DO NOT match"
fi
~~~