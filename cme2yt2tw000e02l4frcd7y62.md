---
title: "Get SSL certificate without a server"
seoTitle: "Get SSL certificate without a server"
seoDescription: "Let's Encrypt can help us create SSL certs, without any online server, using DNS-01 challenge which proves domain ownership through a txt DNS record"
datePublished: Fri Aug 08 2025 15:12:38 GMT+0000 (Coordinated Universal Time)
cuid: cme2yt2tw000e02l4frcd7y62
slug: get-ssl-certificate-without-a-server
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/mT7lXZPjk7U/upload/9470cc6ec1bd30bbed3c6599f899efce.jpeg
tags: dns, cloudflare, ssl, letsencrypt, tls, certbot, eff

---

## **What You’ll Need**

* A domain name
    
* Control over its DNS (via your registrar or DNS hosting provider)
    
* A machine to run commands on (your laptop is fine)
    
* (Optional but easier) API access for your DNS provider
    

## **Step 1 — Install Certbot and the Right DNS Plugin**

Certbot is the tool that talks to Let’s Encrypt. Install it along with your DNS provider plugin.

In this article, we’re gonna be using Cloudflare as our DNS provider, so for example:

```bash
sudo apt install certbot python3-certbot-dns-cloudflare
```

Find your provider’s plugin here: [https://certbot.eff.org/docs/using.html#dns-plugins](https://certbot.eff.org/docs/using.html#dns-plugins)

## **Step 2 — Create DNS API Credentials**

Get an API token/key from your DNS provider that:

* Can **edit DNS records** for your domain
    
* Nothing else (keep it limited)
    

Then, save it on your computer:

```bash
mkdir -p ~/.secrets/certbot
nano ~/.secrets/certbot/cloudflare.ini
```

Inside the file:

```bash
dns_cloudflare_api_token = your_api_token_here
```

After that, secure the file:

```bash
chmod 600 ~/.secrets/certbot/cloudflare.ini
```

## **Step 3 — Request the Certificate**

Now it’s time for the main command run:

```bash
sudo certbot certonly \
  --dns-cloudflare \
  --dns-cloudflare-credentials ~/.secrets/certbot/cloudflare.ini \
  -d 'example.com' -d '*.example.com'
```

> Note: Change `‘example.com‘` and `’*.example.com’` to your domain.

Now you may ask, What’s happening?

* `certonly` → Get the cert without running a server
    
* `--dns-cloudflare` → Use DNS verification
    
* `-d` → Your domain(s); `*.example.com` gets you a wildcard cert
    

## **Step 4 — Locate Your Certificate Files**

Once done, your certs are here:

```bash
/etc/letsencrypt/live/example.com/fullchain.pem   # Certificate
/etc/letsencrypt/live/example.com/privkey.pem     # Private key
```

You can now use these on a CDN, email server, reverse proxy, IoT device, etc.

## **Step 5 — Renewing the Certificate**

Since DNS-01 doesn’t depend on a live web server, renewal is easy:

```bash
sudo certbot renew
```

If your DNS plugin uses API credentials, renewal can be fully automated.

You now have a valid SSL/TLS certificate for your domain — without a server.