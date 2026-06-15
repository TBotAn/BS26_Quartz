---
tags:
  - truenas
  - local
  - nextcloud
---

## 1. Follow Lawrence Systems Video

Follow the following [video](https://youtu.be/8Cxg1mAYtL8)

## 2. Make sure Tailscale Is installed

This is to avoid having to expose a port in the network for remote access, is preferable to have a dedicated VPN like tailscale to secure the access to the local network.

## 3. Start by Creating the Datasets

Make sure to create each dataset as nextcloud can get confused if we save it to the same dataset

![[Pasted image 20260615113045.png]]


## 4. Install App 

On installing the app, if there are issues when installing tick **Automatic Permission** on the paths.


## 5. Untrusted Domain Fix
![[Pasted image 20260615115104.png]]

1. Go to truenas scale apps dashboard
2. find the nextcloud app, click the three dots (`...`) and select edit.
3. In the Host parameter enter the IP:PORT link into it this will make the local work
4. (FOR REMOTE ACCESS) Add your IP to host filed or environment variables 
	1. Log into to tailscale 
	2. Find the TrueNas Server
	3. Copy the 100.x.x.x Address - Right next to your TrueNAS server's name, you will see an IP address starting with `100.`. Click on it to copy it. _(This replaces the `100.x.x.x` placeholder)_.
	4. Copy the MagicDNS Name - Click directly on your TrueNAS server's name to open its detailed page. Under the **General** section, look for **Full domain**. It will look exactly like `your-nas.your-tailnet.ts.net`.