---
tags:
  - truenas
  - local
---

## 1. Install AdGuard on TrueNAS Scale

![[Pasted image 20260613164514.png]]

Start by creating a dataset inside the "configs" or "appconfig" folder. Don't forget to change the permissions to allow the apps group/user.

![[Pasted image 20260613164758.png]]



## 2. Setup Router

1. Go to http://192.168.1.1/
2. Login with the router credentials
3. Go to Local Network > LAN > DHCP Server
   ![[Pasted image 20260613170129.png]]
4. Click to turn off ISP DNS.
5. As soon as you click **Off**, two new blank entry fields will magically appear right below it labeled something like _Primary DNS_ and _Secondary DNS_ (or _DNS Server 1 / 2_).
6. In the new **Primary DNS** box that appears, type in your **TrueNAS SCALE IP address**
7. In the **Secondary DNS** box, you can either leave it blank or type a fast public backup like `1.1.1.1` (Cloudflare)
8. Click the blue **Apply** button at the bottom right.

## 3. Fix the IPv6 Leak 

![[Pasted image 20260614113618.png]]


1. Change **DNS Delegate Type** from _Auto_ to **Manual**.
   
2. Once you click **Manual**, new input boxes will appear below it asking for IPv6 DNS addresses.
   
3. **If you don't know your TrueNAS IPv6 address:** Leave those new DNS boxes completely blank or filled with zeros (if it lets you). This forces your router to stop handing out IPv6 DNS entirely, forcing your phone to use the perfectly configured IPv4 AdGuard address we set up earlier.
   
4. Click the blue **Apply** button at the bottom.

![[Pasted image 20260614113904.png]]

For a forced approach just turn off the server completly
## 4. Change the RA Service settings

![[Pasted image 20260614115059.png]]

 1. Change the **RA Service** radio button from _On_ to **Off**.
 2. Look slightly lower at the **O** flag setting. It is currently set to _On_. Change **O** to **Off** as well (this stops the router from telling devices to look elsewhere for extra config info).

## 5. Uncheck Port Control

![[Pasted image 20260614115232.png]]

1. Click the **All Off** link at the very bottom left of that grid.
   
2. This should automatically uncheck every single **DHCPv6** and **RA** box for LAN1-LAN4 and SSID1-SSID8. If it doesn't, manually uncheck all of them.
   
3. Click the blue **Apply** button at the bottom right to lock in the changes.


## 6. Checking in linux what DNS system is using

``` bash
resolvectl status
```

``` bash
sudo resolvectl flush-caches
```

``` bash
sudo systemctl restart NetworkManager
```


## 7. Setup for phones

Android phones love to bypass local networks using a feature called **Private DNS**. We need to turn that off and assign your TrueNAS IP manually.

1. Turn off Private DNS:
	1. Open your phone's **Settings**.
	2. Search for **"Private DNS"** (usually under _Connections_ or _Network & Internet_).
	3. Change it from _Automatic_ to **Off**.
2. Hardcode your AdGuard DNS:
	1. Go to **Settings** -> **Wi-Fi**
	2. Press the **Gear Icon** next to your home Wi-Fi network and tap **View More** or **Advanced**.
	3. Change **IP Settings** from _DHCP_ to **Static**.
	4. Keep your IP address the same, but scroll down to **DNS 1**.
	5. Change **DNS 1** to: `192.168.1.158`
	6. Clear out **DNS 2** entirely (leave it blank or `0.0.0.0`).
	7. Save the settings.


