---
title: "Unforce Google SafeSearch"
seoTitle: "Unforce Google SafeSearch"
seoDescription: "Recently, the Iranian government has made changes in the national DNS servers, which causes all DNS requests for Google to be sent to the SafeSearch domain"
datePublished: Fri Aug 04 2023 23:50:38 GMT+0000 (Coordinated Universal Time)
cuid: clkx8o3ta00020ajv9icr4cd1
slug: unforce-google-safesearch
canonical: https://github.com/AliAlmasi/unforce-safesearch
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691192901204/a3914e33-c22f-43e3-ad3c-1bcebc148797.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1691192968218/5a549b5e-c4ed-4f52-aaee-9d8e09ea3f4b.jpeg
tags: dns, google, networking, iran

---

Recently, the Iranian government [has made changes](https://digiato-com.translate.goog/article/2022/07/12/safesearch-internet-mobile?_x_tr_sl=fa&_x_tr_tl=en&_x_tr_hl=en&_x_tr_pto=wapp) in the national DNS servers, which causes all DNS requests for Google to be sent to the domain [`forcesafesearch.google.com`](http://forcesafesearch.google.com) (to IP `216.239.38.120`), which forces all Google users, regardless of their settings, to use Google with SafeSearch.

## How to bypass this?

To bypass this, the system must manually introduce Google's regular search servers ([`google.com`](http://google.com)  -  `142.250.180.142`). For this, it is necessary to use the `hosts` file available in the operating systems to introduce the IP directly to the system so that it does not request Google's safe search from the country's DNS.

> Notice: This solution only works in Windows, macOS and Linux.

## For Windows users

On Windows, you need to open the Run window (*WinKey + R*) and type this as administrator:

```plaintext
notepad C:\Windows\System32\Drivers\etc\hosts
```

This will open the `hosts` file of your Windows on a Notepad.

Next, you need to add these lines at the end of the file:

```plaintext
142.250.180.142 google.com
142.250.180.142 www.google.com
```

Save the file afterward, open cmd and flush the DNS cache by running

```powershell
ipconfig /flushdns
```

Now you're all done. Check if it's working by opening [google.com](http://google.com), or run `nslookup` [`google.com`](http://google.com) on cmd and see what IP it returns.

## For macOS users

Open Terminal and run

```bash
sudo nano /private/etc/hosts
```

Since we use sudo to edit the hosts file, you will be asked to enter the administrator password of your macOS user account. Type your admin password and hit the Enter key.

> Note: The cursor doesn’t work in the command line. You'll need to use the arrow keys to navigate between the lines inside the hosts file.

Paste these lines at the end of the file:

```plaintext
142.250.180.142 google.com
142.250.180.142 www.google.com
```

After that, press *CTRL + X* on your keyboard. Enter Y to save the changes, and hit the Enter button.

Then, you'll need to flush the DNS cache. to do this, if you're using macOS Monterey or Big Sur, run this:

```bash
sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder
```

Else, if you're using macOS Catalina, Mojave, High Sierra, Sierra, Mountain Lion or Lion, run this:

```bash
sudo killall -HUP mDNSResponder
```

Now you're all done. Check if it's working by opening [google.com](http://google.com), or run `nslookup` [`google.com`](http://google.com) on your Terminal and see what IP it returns.

## For Linux users

Open Terminal and run this:

```bash
sudo nano /etc/hosts
```

Enter the password for sudo when asked.

Paste these lines at the end of the file:

```plaintext
142.250.180.142 google.com
142.250.180.142 www.google.com
```

After that, press *CTRL + X* on your keyboard. Enter Y to save the changes, and hit the Enter button.

Then, to flush the DNS cache on Linux, if you are using `systemd-resolved`, you can use the command followed by `--flush-caches`.  
Alternatively, you can use the `resolvectl` command followed by the `flush-caches` option.

```plaintext
sudo systemd-resolve --flush-caches
sudo resolvectl flush-caches
```

Now you're all done. Check if it's working by opening [google.com](http://google.com), or run `nslookup` [`google.com`](http://google.com) on your Terminal and see what IP it returns.