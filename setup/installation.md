---
icon: asterisk
description: To setup Proxmox VE for the first time on a local machine.
---

# Installation

***

### Prerequisites

* Download [Proxmox Virtual Environment (PVE) ISO](https://www.proxmox.com/en/downloads).
* Create a bootable PVE on a USB drive with [Ventoy](https://www.ventoy.net/en/download.html).
* Boot into PVE setup using Normal Mode.
* Set the disk format to `zfs` if RAM is at least 64GB.  Else `ext4`.
* Set the server IP and gateway IP. Check on Windows with `ipconfig`.



***

### Post-Installation

* Configure repositories with [PVE Post Install Script](https://tteck.github.io/Proxmox/#proxmox-ve-post-install). \
  Alternatively:

{% code overflow="wrap" fullWidth="false" %}
```bash
wget --no-cache -qO- https://raw.githubusercontent.com/therepos/proxmox/main/installers/install-postpve.sh | bash
```
{% endcode %}

* Install Nvidia Driver.

{% code overflow="wrap" %}
```bash
wget --no-cache -qO- https://raw.githubusercontent.com/therepos/proxmox/main/installers/install-nvidiadriver.sh | bash
```
{% endcode %}

* Install Nvidia Container Toolkit.

{% code overflow="wrap" %}
```bash
wget --no-cache -qO- https://raw.githubusercontent.com/therepos/proxmox/main/installers/install-nvidiact.sh | bash
```
{% endcode %}

* Install Docker.

{% code overflow="wrap" %}
```bash
curl -fsSL https://raw.githubusercontent.com/therepos/proxmox/main/installers/install-docker.sh | bash
```
{% endcode %}

* Install [Cloudflared](https://tteck.github.io/Proxmox/#cloudflared-lxc).&#x20;
