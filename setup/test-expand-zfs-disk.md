---
description: To expand ZFS partition.
---

# Disk Partitions

***

### **Resize Partitions**

* Use the `parted` tool to resize the partitions. Open `parted` for the disk:

```bash
bashCopy codeparted /dev/nvme1n1
```

* Print the current partition table: In the `parted` prompt, type:

```bash
bashCopy codeprint
```

* Identify the partition number (e.g. `p3`) to resize it to use all remaining space on the disk.&#x20;

```bash
bashCopy coderesizepart 3 100%
```

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

* Run the following command to grow the `rpool` and make it use the newly resized partitions:

```bash
bashCopy codezpool online -e rpool nvme-eui.ace42e003554b1072ee4ac0000000001-part3
zpool online -e rpool nvme-eui.0000000624098476caf25b0320000086-part3
```

### **Verify the Expansion**

* After running the above commands, check the pool's status to confirm the expanded capacity:

```bash
bashCopy codezpool list
```

