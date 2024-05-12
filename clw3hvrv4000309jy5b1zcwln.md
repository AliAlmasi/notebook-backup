---
title: "How to use YeBeKhe's Telegram V2ray Collector"
seoTitle: "How to use YeBeKhe's Telegram V2ray Collector"
seoDescription: "YeBeKhe's new open-source project is so cool! You can use V2ray configurations from shared configs over the Telegram channels."
datePublished: Sun May 12 2024 12:11:55 GMT+0000 (Coordinated Universal Time)
cuid: clw3hvrv4000309jy5b1zcwln
slug: telegram-v2ray-collector
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1715514014949/a4d59d82-05e5-437a-9bd3-851fdbe9d651.png
tags: opensource, internet, telegram, xray, v2ray, filternet, hiddify, internet-censorship

---

This project, as its name already tells, collects V2ray configurations from over 70 Telegram channels. This project can help people in Iran to avoid the systematic censorship of the Internet.

[YeBeKhe's Telegram V2ray Collector](https://github.com/yebekhe/TelegramV2rayCollector) is loaded and served on GitHub.

[![](https://cdn.hashnode.com/res/hashnode/image/upload/v1698686343248/cdbebe76-57e6-42e2-a87b-59a30b8be78f.png align="center")](https://github.com/yebekhe/TelegramV2rayCollector)

This project is updated hourly, so people can use "fresh" configs and circumvent the censorship more easily. You can use this project by adding its subscription link to your V2ray/Xray client program and you can update it every hour.

I'm going to use [***Hiddify Next***](https://github.com/hiddify/hiddify-next) to show you how you can use Telegram V2ray Collector. *Hiddify Next* is available to install on Windows, Linux and Android devices (Also available on Google Play and Microsoft Store).

First, install this program so you can use proxy subscriptions. You can install *Hiddify Next* on any desktop operating system (Also [available on AUR](https://aur.archlinux.org/packages/hiddify-next-bin) for Arch Linux users). if you need any documentation or guides on installing it, you can [visit their website](https://hiddify.com/app/).

You may install and use any V2ray/Xray client program you like to (e.g. v2rayN on Windows, or v2rayNG on Android), as they all use the same [V2ray](https://github.com/v2ray/v2ray-core)/[Xray](https://github.com/XTLS/Xray-core) core.

After setting up our client program, we copy the subscription link from the readme file in their GitHub repo.

![As you can see, there are subscription link for most popular proxy cores like Xray, Singbox, Clash and Surfboard.](https://cdn.hashnode.com/res/hashnode/image/upload/v1715509127290/a0e045af-a8be-4eb0-bf4e-972911f839f4.png align="left")

As you can see, there are subscription link for most popular proxy cores like Xray, Singbox, Clash and Surfboard.

> The "Donate" links are for proxies that have been donated to the project. They're included in the "Group Mix" links, so you may only copy the "Group Mix" link.

![There's also different subscription links for different types of proxies such as Vless, Vmess, Reality, Trojan, Shadowsocks, Tuic and Hysteria.](https://cdn.hashnode.com/res/hashnode/image/upload/v1715509249252/1f721988-496e-4e34-aed9-7724c6f456fe.png align="left")

There's also different subscription links for different types of proxies such as Vless, Vmess, Reality, Trojan, Shadowsocks, Tuic and Hysteria for different types of proxy cores; But we're not gonna be picky about types of proxies, so we use the mixed subscription links (the ones in the previous screenshot - *"Group Mix Link"*).

I've setup *HN* which uses Xray core, so we have to copy the Xray subscription links. You may either use the raw subscription, or the *Base64* subscription.

The difference between raw *(plaintext)* subscription and the *Base64* subscription is that when you open the [raw subscription link](https://raw.githubusercontent.com/yebekhe/TelegramV2rayCollector/main/sub/normal/mix), you can see the information that link contains, but Base64 subscription link's information are encoded. Base64 may be helpful in networks where traffic is being constantly scanned and sniffed.

I personally use the Base64 subscription link, so we're gonna copy the [**Xray (Base64)Group Mix link**](https://raw.githubusercontent.com/yebekhe/TelegramV2rayCollector/main/sub/base64/mix)**.***(you can copy the link by right clicking on*[*here*](https://raw.githubusercontent.com/yebekhe/TelegramV2rayCollector/main/sub/base64/mix)*and then select "Copy link")*

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715513142406/e163392a-3c11-4334-9771-6c7da13ddafc.png align="left")

---

After copying subscription link, we need to import it into our client program. On *Hiddify Next* it's easy as pie, you just start the program and click on "New Profile" on the home screen;

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715514353521/cb1d154b-a062-4f02-b065-afa0115043e8.png align="center")

Then you select "Add from clipboard" and then you wait for the program to read and import the link you copied. At the end you'll see this:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715514426790/8533d0f0-6703-4954-bd59-5c8d44ed945c.png align="center")

Now you can easily use this service and have "fresh" V2ray configs anytime you want so you can circumvent the censorship more easily. Updating the subscription is also very easy. You just click on this button here and then you'll have new configs. Remember, this subscription updates hourly

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1715514664403/74a6387a-4fdd-4584-8554-e124a02a85ff.png align="center")

---

Instructions on Android version of *Hiddify Next* is also like the desktop version, as they both have same interface.

If you have any questions about *Hiddify Next*, you can ask them in the [discussion section of their GitHub repo](https://github.com/hiddify/hiddify-next/discussions). If you found any bugs or issues, you can inform the team by submitting an issue in the [issues section of their GitHub repo](https://github.com/hiddify/hiddify-next/issues).