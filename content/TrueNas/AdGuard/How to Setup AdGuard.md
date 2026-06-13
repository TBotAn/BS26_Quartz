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
