---
title: Using OpenSSL to Validate a Key Pair Match
modified: 2016-12-18
tags: [tls,ssl,openssl]
layout: post
---
The following bash script will validate if a PEM formatted key pair match or not.

{% highlight bash %}
export FQDN=DOMAIN_TO_VALIDATE
export C=$(openssl x509 -noout -modulus -in ${FQDN}.cer | openssl md5)
export K=$(openssl rsa -noout -modulus -in ${FQDN}.key | openssl md5)
if [[ $(diff <(echo ${C}) <(echo ${K}) | wc -l) -eq 0 ]]; then
    echo "Key pair match"
else
    echo "Key pair DO NOT match"
fi
{% endhighlight %}
