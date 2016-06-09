---
layout: post
title:  NGINX SSL on OS X with a letsencrypt cert
---

Certbot (https://github.com/certbot/certbot) is the client previously known as the "Let's Encrypt Client." I'm using it on my OS X machine to provide a free SSL cert for an NGINX SSL termination instance.

As of last week (June 6, 2016), there was still a [bug](https://github.com/certbot/certbot/issues/3120) in the header generation for OS X that would prevent the client from working, the fix was to not allow the client to update itself.

Once you walk through the usual [letsencrypt setup](https://certbot.eff.org/) choosing `certonly`, you may need to use the `standalone` auth mechanism if you're running NGINX on a port other than the default (443).

Your certs will be output to `/etc/letsencrypt/live/www.yourhostname.com/` so set up links for nginx.conf

```
$ cd /usr/local/etc/nginx
$ sudo ln -s /etc/letsencrypt/live/www.yourhostname.com/privkey.pem ssl-nopw.key
$ sudo ln -s /etc/letsencrypt/live/www.yourhostname.com/fullchain.pem ssl-unified.crt
```

resulting in

``` 
rwxr-xr-x  1 root   admin    47  8 Jan 20:52 ssl-nopw.key -> /etc/letsencrypt/live/www.yourhostname.com/privkey.pem
lrwxr-xr-x  1 root   admin    49  8 Jan 20:52 ssl-unified.crt -> /etc/letsencrypt/live/www.yourhostname.com/fullchain.pem
```

and the corresponding `nginx.conf` entry:

```  
    server {
        listen       443 ssl;
        server_name  www;
        ssl_certificate      ssl-unified.crt;
        ssl_certificate_key  ssl-nopw.key;
        [...]
    }
````

## References
1. [Where to set NGINX SSL settings in `nginx.conf`](https://www.nginx.com/resources/admin-guide/nginx-ssl-termination/)
1. [Setting up automatic check with launchctl](http://launched.zerowidth.com/)