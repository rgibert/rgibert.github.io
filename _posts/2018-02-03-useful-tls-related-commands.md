---
title: Useful TLS related commands
modified: 2018-02-03
tags: [tls,pem,pkcs12,jks,openssl,keytool]
layout: post
---

Generating a self-signed key pair

{% highlight bash %}
openssl \
  req \
    -nodes \
    -x509 \
    -newkey rsa:4096 \
    -keyout key.pem \
    -out certificate.pem \
    -days 365 \
    -subj "/C=COUNTRY/ST=STATE/L=CITY/O=COMPANY/OU=ORG/CN=FQDN"
{% endhighlight %}

Converting PEM to PKCS12

{% highlight bash %}
openssl \
  pkcs12 \
    -export \
    -out output.pkcs12 \
    -in certificate.pem \
    -inkey key.pem
{% endhighlight %}

Converting PKCS12 to JKS

{% highlight bash %}
keytool \
  -importkeystore \
  -srckeystore input.pkcs12 \
  -srcstoretype PKCS12 \
  -destkeystore output.jks \
  -deststoretype JKS
{% endhighlight %}
