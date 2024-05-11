---
title: "Easy VLESS config with CF Worker"
seoDescription: "Configuring VLESS with CF Worker Made Easy. Just create a CF Worker and then copy & paste all of the worker.js file's content as the worker's configuration"
datePublished: Sat Aug 05 2023 00:04:33 GMT+0000 (Coordinated Universal Time)
cuid: clkx9609p000109mtevm5chfi
slug: easy-vless-config-with-cf-worker
canonical: https://github.com/AliAlmasi/vless-cf-worker
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691193812695/0ce813c9-1943-4dbe-b874-3ad156196251.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1691193833480/66aaa0ae-3f2d-4377-99e4-037f24e8a9df.jpeg
tags: cloudflare, websockets, iran, cloudflare-worker, filternet

---

### [نسخه فارسی این نوشته اینجاست](https://fa.note.al1almasi.ir/easy-vless-config-with-cf-worker)

## How to use this?

It's Super easy (you don't need any server). Just create a CF Worker and then copy & paste all of the [worker.js file's content](https://raw.githubusercontent.com/AliAlmasi/vless-cf-worker/main/worker.js) as the worker's configuration, then do all of these things:

1. Generate a UUID and replace the one in the worker's configuration after you paste it ([line 201](https://github.com/AliAlmasi/vless-cf-worker/blob/main/worker.js#L201)).
    
2. Save & Deploy.
    
3. OPTIONAL: If you've got a domain on your Cloudflare, add a custom domain for your worker.
    
4. Create a VLESS configuration on any V2Ray/Xray program that you use (personally, I prefer [v2rayN](https://github.com/2dust/v2rayN))
    
5. Set TLS as **TLS** and your worker's domain as the SNI.
    
6. Set transport to **ws**.
    
7. Set your worker's domain as the ws host.
    
8. Set any *Clean Cloudflare IP* as the destination address. You can use [IRCF.space](http://IRCF.space).
    
9. Set **443** as port.
    
10. And finally, set your own generated UUID as the configuration's UUID.
    

Now you're all done. Test your VLESS configuration.

![](https://github.com/AliAlmasi/vless-cf-worker/raw/main/screenshots/vless-config.jpg align="left")