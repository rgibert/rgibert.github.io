---
title: Simplifying Apache httpd setup with mod_macro
tags:
    - code
    - httpd
---

For Apache httpd setups with numerous virtual hosts there can be a lot of config redundancy. This can be alleviated by using mod_macro (as of httpd 2.4.6 this is a default Apache httpd module, for older versions it can be downloaded from https://people.apache.org/~fabien/mod_macro/).

Here are my configs using mod_macro (currently I run httpd 2.2.x, these configs are made for this version of httpd). This assumes you have a central web root of /home/web/DOMAIN/SUBDOMAIN, so subdomain.domain.com would be at /home/web/domain.com/subdomain.

First a common macro for all virtual hosts:

~~~ conf
<Macro vhost-common $subdomain $domain>
    ServerAdmin webmaster@$domain
    ServerName $subdomain.$domain
    DocumentRoot /home/web/$domain/$subdomain/htdocs/
    LogLevel error
    ErrorLog "|rotatelogs /home/web/$domain/$subdomain/logs/error.%Y%m%d.log 86400"
    CustomLog "|rotatelogs /home/web/$domain/$subdomain/logs/access.%Y%m%d.log 86400" combined

    <IfModule mod_rewrite.c>
        RewriteLogLevel 0
        RewriteLog "|rotatelogs /home/web/$domain/$subdomain/logs/rewrite.%Y%m%d.log 86400"
    </IfModule>
    <IfModule mod_jk.c>
        JkLogLevel info
        JkLogFile "|rotatelogs /home/web/$domain/$subdomain/logs/mod_jk.%Y%m%d.log 86400"
    </IfModule>
    <Directory />
        order deny,allow
        deny from all
    </Directory>
    <Directory /home/web/$domain/$subdomain>
        order allow,deny
        allow from all
    </Directory>
    Header always set X-Frame-Options DENY
    Header always set X-Content-Type-Options nosniff
</Macro>
~~~

Next we need a config that is used for any HTTP vhost:

~~~ conf
<Macro vhost-http $subdomain $domain $port>
    <VirtualHost *:$port>
        Use vhost-common $subdomain $domain
    </VirtualHost>
</Macro>
~~~

And a config that is used for any HTTPS vhost:

~~~ conf
<Macro vhost-https $subdomain $domain $port>
    <IfModule mod_ssl.c>
    <VirtualHost *:$port>
        Use common $subdomain $domain

        SSLEngine on
        SSLProtocol all -SSLv2 -SSLv3
        SSLHonorCipherOrder on
        SSLCipherSuite ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:ECDH+3DES:DH+3DES:RSA+AESGCM:RSA+AES:RSA+3DES:!aNULL:!MD5:!DSS
        SSLCompression Off
        SSLCertificateFile /home/web/$domain/$subdomain/ssl/$subdomain.$domain.pem
        SSLCertificateKeyFile /home/web/$domain/$subdomain/ssl/$subdomain.$domain.key
        SSLCACertificateFile /home/web/$domain/$subdomain/ssl/cas.pem

        BrowserMatch "MSIE [2-6]" \
            nokeepalive ssl-unclean-shutdown \
            downgrade-1.0 force-response-1.0
        # MSIE 7 and newer should be able to use keepalive
        BrowserMatch "MSIE [17-9]" ssl-unclean-shutdown
    </VirtualHost>
    </IfModule>
</Macro>
~~~

VirtualHosts can then be spun up with just:

~~~ conf
Use vhost-http subdomain domain.com 80
~~~

or

~~~ conf
Use vhost-https subdomain domain.com 443
~~~
