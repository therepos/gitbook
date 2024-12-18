---
description: To expand ZFS partition.
---

# Disk Partitions

### **Resize Partitions**

Use the `parted` tool to resize the partitions. \
Follow these steps for each disk (`nvme1n1` and `nvme0n1`):

* Open `parted` for the disk:

```bash
bashCopy codeparted /dev/nvme1n1
```

* Print the current partition table: In the `parted` prompt, type:

```bash
bashCopy codeprint
```

* Resize the partition (`p3`):

```bash
bashCopy coderesizepart 3 100%
```

This resizes the third partition to use all remaining space on the disk. Type `Yes` if prompted for confirmation.

* Exit `parted`:

```bash
bashCopy codequit
```

* Repeat these steps for the second disk (`nvme0n1`):

```bash
bashCopy codeparted /dev/nvme0n1
```

* Follow the same commands to resize `p3` on this disk.

### **Expand the ZFS Pool**

Run the following command to grow the `rpool` and make it use the newly resized partitions:

```bash
bashCopy codezpool online -e rpool nvme-eui.ace42e003554b1072ee4ac0000000001-part3
zpool online -e rpool nvme-eui.0000000624098476caf25b0320000086-part3
```

### **Verify the Expansion**

After running the above commands, check the pool's status to confirm the expanded capacity:

```bash
bashCopy codezpool list
```

