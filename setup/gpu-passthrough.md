---
icon: asterisk
description: To passthrough dedicated graphics card to a VM.
---

# GPU Passthrough

This page is intended to document the steps for NVIDIA GPU passthrough.

```bash
// Some code
nano /etc/default/grub
GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on"
update-grub
nano /etc/modules

vfio
vfio_iommu_type1
vfio_pci
vfio_virqfd

reboot
dmesg | grep -e DMAR -e IOMMU
nano /root/check-iommu.sh

#!/bin/bash
for d in /sys/kernel/iommu_groups/*/devices/*; do
    n=${d#/sys/kernel/iommu_groups/*}
    n=${n%%/*}
    printf 'IOMMU Group %s ' "$n"
    lspci -nns "${d##*/}"
done;

chmod +x /root/check-iommu.sh
/root/check-iommu.sh

Note their PCI addresses e.g. 01:00.0[10de:2571](GPU) and 01:00.1 [10de:228e](audio).

nano /etc/modprobe.d/vfio.conf
options vfio-pci ids=10de:2571,10de:228e
update-initramfs -u
reboot

lspci -nnk -d 10de:2571
lspci -nnk -d 10de:228e

```

