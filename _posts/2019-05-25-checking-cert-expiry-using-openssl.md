---
title: Checking certificate expiry using openssl
modified: 2019-05-24
tags: [tls,openssl]
layout: post
---

The following command will connect to a TLS endpoint using OpenSSL and return the expiry date for the certificate for that endpoint.

{% highlight bash %}
openssl s_client -connect HOST:PORT 2>/dev/null <<< "Q" | openssl x509 -text | grep "Not After :"
{% endhighlight %}
