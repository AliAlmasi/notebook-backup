---
title: "Unforce Google SafeSearch"
seoTitle: "Unforce Google & Bing SafeSearch"
seoDescription: "The Iranian government has made changes in the national DNS servers, which causes all requests for Google to be sent to a "SafeSearch-forced" Google"
datePublished: Fri Aug 04 2023 23:50:38 GMT+0000 (Coordinated Universal Time)
cuid: clkx8o3ta00020ajv9icr4cd1
slug: unforce-safesearch
canonical: https://github.com/AliAlmasi/unforce-safesearch
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691192901204/a3914e33-c22f-43e3-ad3c-1bcebc148797.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1691192968218/5a549b5e-c4ed-4f52-aaee-9d8e09ea3f4b.jpeg
tags: dns, google, networking, iran, bin

---

### [Persian - لینک نسخه فارسی این نوشته](https://fa.note.al1almasi.ir/unforce-safesearch)

Recently, the Iranian government [has made changes](https://digiato-com.translate.goog/article/2022/07/12/safesearch-internet-mobile?_x_tr_sl=fa&_x_tr_tl=en&_x_tr_hl=en&_x_tr_pto=wapp) in the national DNS servers, which causes all DNS requests for Google to be sent to the domain `forcesafesearch.google.com` (to IP `216.239.38.120`), which forces all Google users, regardless of their settings, to use Google with the SafeSearch on.

## UPDATE - BING IS POISONED TOO:

[This user's issue](https://github.com/AliAlmasi/unforce-safesearch/issues/1) shows that not only Google, but also Bing has been forcibly placed on SafeSearch for Iranian users. Therefore, we put the necessary codes to bypass the restriction placed on Bing inside this text. If you have done the settings related to Google in the past, you can only put the part related to Bing in the `resolv.conf` file in Linux and Mac or `hosts` file in Windows.

If you see similar problems regarding forcing SafeSearch for Iranian users on other search engines, you can register the case in the Issues section of this repository so that it can be included in this guide. Your contribution may help many people behind Iran's Filternet.

## How to bypass this?

To bypass this, the system must manually introduce Google's regular search servers (`google.com`  -  `142.250.180.142`). For this, it is necessary to use the `hosts` file available in the operating systems to introduce the IP directly to the system so that it does not request Google's safe search from the country's DNS.

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
13.107.21.200 bing.com
13.107.21.200 www.bing.com
```

Save the file afterward, open cmd and flush the DNS cache by running

```plaintext
ipconfig /flushdns
```

Now you're all done. Check if it's working by opening [google.com](https://google.com), or run `nslookup google.com` on cmd and see what IP it returns.

## For macOS users

Open Terminal and run

```plaintext
sudo nano /private/etc/hosts
```

Since we use sudo to edit the hosts file, you will be asked to enter the administrator password of your macOS user account. Type your admin password and hit the Enter key.

> Note: The cursor doesn’t work in the command line. You'll need to use the arrow keys to navigate between the lines inside the hosts file.

Paste these lines at the end of the file:

```plaintext
142.250.180.142 google.com
142.250.180.142 www.google.com
13.107.21.200 bing.com
13.107.21.200 www.bing.com
```

After that, press *CTRL + X* on your keyboard. Enter Y to save the changes, and hit the Enter button.

Then, you'll need to flush the DNS cache. to do this, if you're using macOS Monterey or Big Sur, run this:

```plaintext
sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder
```

Else, if you're using macOS Catalina, Mojave, High Sierra, Sierra, Mountain Lion or Lion, run this:

```plaintext
sudo killall -HUP mDNSResponder
```

Now you're all done. Check if it's working by opening [google.com](https://google.com), or run `nslookup google.com` on your Terminal and see what IP it returns.

## For Linux users

Open Terminal and run this:

```plaintext
sudo nano /etc/hosts
```

Enter the password for sudo when asked.

Paste these lines at the end of the file:

```plaintext
142.250.180.142 google.com
142.250.180.142 www.google.com
13.107.21.200 bing.com
13.107.21.200 www.bing.com
```

After that, press *CTRL + X* on your keyboard. Enter Y to save the changes, and hit the Enter button.

Then, to flush the DNS cache on Linux, if you are using `systemd-resolved`, you can use the command followed by `--flush-caches`.  
Alternatively, you can use the `resolvectl` command followed by the `flush-caches` option.

```plaintext
sudo systemd-resolve --flush-caches
sudo resolvectl flush-caches
```

You can also restart the *nscd* if you're using that, by running this command:

```plaintext
sudo /etc/init.d/nscd restart
```

Now you're all done. Check if it's working by opening [google.com](https://google.com), or run `nslookup google.com` on your Terminal and see what IP it returns.