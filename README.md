# Nginx Recipes For The Lazy

Tested on Ubuntu 16.04 and 18.04

## Static Server

[`static.conf`](sites-available/static.conf)

## Static Server for Clientside Routers (React, Angular, Vue.js, ...)

[`spwa.conf`](sites-available/spwa.conf)

## HTTP Proxy Server (Node.js, Python, ...)

[`proxy.conf`](sites-available/static.conf)

## PHP Proxy Server

[`php.conf`](sites-available/php.conf)

## WordPress Server

[`wordpress.conf`](sites-available/wordpress.conf)

# SSL

LetsEncrypt [certbot.eff.org](https://certbot.eff.org/)

## Wildcard Certificate with Cloudflare

```sh
certbot certonly \
    --preferred-challenges dns-01 \
    --dns-cloudflare --dns-cloudflare-credentials /root/.cloudflare.ini \
    -d 'example.com,*.example.com'

# Renewal
certbot renew \
    --dns-cloudflare --dns-cloudflare-credentials /root/.cloudflare.ini \
    --pre-hook "systemctl stop nginx" \
    --post-hook "systemctl start nginx"
    # REMINDER: --dry-run
```

`/root/.cloudflare.ini`
```ini
dns_cloudflare_email = "me@example.com"
dns_cloudflare_api_key = "abcdefghijklmnopqrstuvwxyz0"
```