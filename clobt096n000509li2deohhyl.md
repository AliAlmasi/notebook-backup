---
title: "RTL8821CE Wireless card fix on Ubuntu (and other Debian/Ubuntu based distros)"
seoTitle: "RTL8821CE Wireless card fix on Linux"
seoDescription: "For some reason, the rtl8821ce WiFi hardware works poorly or not at all on most Linux distros. In this guide, we want to build and install this driver"
datePublished: Sun Oct 29 2023 18:27:50 GMT+0000 (Coordinated Universal Time)
cuid: clobt096n000509li2deohhyl
slug: rtl8821ce-wireless-card-fix-on-ubuntu
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1698606945833/60033043-1cd9-4ba0-8e33-b15e2bb48d43.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1698606916986/64c8af00-06ed-4b65-8e44-59ef0fb7362d.jpeg
tags: ubuntu, linux, debian, foss, wireless-network

---

### [لینک نسخه فارسی این نوشته](https://fa.note.al1almasi.ir/rtl8821ce-wireless-card-fix-on-ubuntu)

For some reason, the rtl8821ce WiFi hardware works poorly or not at all on most Linux distros. The driver used in the Linux kernel for this hardware is outdated or for other reasons that I don't know about, it doesn't work properly. The solution to this problem is a driver developed by [a friend from Portugal](https://github.com/tomaspinho) and placed on GitHub.

**In this guide, we want to build and install this driver on our Ubuntu.**

> Warning: Before proceeding, take a snapshot of your system for safety.

Open a Terminal and follow along:

1. Update your APT: `sudo apt update`
    
2. Install the necessary tools: `sudo apt install bc module-assistant build-essential dkms git`
    
3. Remove the `rtl8821ce-dkms` if it is present: `sudo apt remove rtl8821ce-dkms`
    
4. Clone the driver and get in the directory of the cloned driver: `git clone`[`https://github.com/tomaspinho/rtl8821ce.git`](https://github.com/tomaspinho/rtl8821ce.git)`&& cd rtl8821ce`
    
5. Prepare/Build the driver: `sudo m-a prepare`
    
6. If the output has `Couldn't create the /usr/src/linux symlink!`, try again
    
7. Install the driver: `sudo ./`[`dkms-install.sh`](http://dkms-install.sh)
    
8. Open a new terminal and run: `sudo nano /etc/modprobe.d/blacklist.conf`
    
9. Add `blacklist rtw88_8821ce` to the end and save the file
    
10. Restart the system and... Done!