---
icon: asterisk
description: To configure the network settings in Proxmox for remote access.
---

# Network

When using third-party tunnel for remote access (e.g. Cloudflare), configure your router DNS resolver to a public DNS. This is to avoid conflict between the default DNS set by the ISP and the public DNS used by the tunnel.

#### Public DNS

Google DNS — `8.8.8.8` and `8.8.4.4` \
Cloudflare DNS — `1.1.1.1` and `1.0.0.1` \
OpenDNS — `208.67.222.222` and `208.67.220.220`
