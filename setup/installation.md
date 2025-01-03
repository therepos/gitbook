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
bash -c "$(wget -qLO- https://github.com/therepos/proxmox/raw/main/installers/install-postpve.sh)"
```
{% endcode %}

* Check and format disk drives.

{% code overflow="wrap" %}
```bash
bash -c "$(wget -qLO- https://github.com/therepos/proxmox/raw/main/util/formatdisk.sh)"
```
{% endcode %}

* Install [Filebrowser ](https://tteck.github.io/Proxmox/#file-browser)for navigating files.

***

### Essentials

* Install Nvidia Driver.

{% code overflow="wrap" %}
```bash
bash -c "$(wget -qLO- https://github.com/therepos/proxmox/raw/main/installers/install-nvidiadriver.sh)"
```
{% endcode %}

* Install Docker on Proxmox.

{% code overflow="wrap" %}
```bash
bash -c "$(wget -qLO- https://github.com/therepos/proxmox/raw/main/installers/install-dockerhost.sh)"
```
{% endcode %}

* Install Portainer.

{% code overflow="wrap" %}
```bash
bash -c "$(wget -qLO- https://github.com/therepos/proxmox/raw/main/installers/install-portainer.sh)"
```
{% endcode %}



***

### Optional

* Install [Cloudflared](https://tteck.github.io/Proxmox/#cloudflared-lxc) for remote access.



***

### Utilities

* List all containers, virtual machines, services and dockers.

{% code overflow="wrap" %}
```bash
bash -c "$(wget -qLO- https://github.com/therepos/proxmox/raw/main/util/listworkloads.sh)"
```
{% endcode %}

* Export system information.

{% code overflow="wrap" %}
```bash
bash -c "$(wget -qLO- https://github.com/therepos/proxmox/raw/main/util/getsysinfo.sh)"
```
{% endcode %}

* Setup Samba share.

{% code overflow="wrap" %}
```bash
bash -c "$(wget -qLO- https://github.com/therepos/proxmox/raw/main/util/sambashare.sh)"
```
{% endcode %}

* Mount and unmount drive.

{% code overflow="wrap" %}
```bash
bash -c "$(wget -qLO- https://github.com/therepos/proxmox/raw/main/util/mountdrive.sh)"
```
{% endcode %}

* Backup ZFS to secondary drive.

{% code overflow="wrap" %}
```bash
bash -c "$(wget -qLO- https://github.com/therepos/proxmox/raw/main/util/zfsbackup.sh)"
```
{% endcode %}



***

References

* [GitHub therepos](https://github.com/therepos/proxmox/tree/main/installers)
* [Proxmox VE Helper Scripts](https://tteck.github.io/Proxmox/)
