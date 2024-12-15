# Test : Expand ZFS Disk

#### **Step 4: Resize Partitions**

We will use the `parted` tool to resize the partitions. Follow these steps for each disk (`nvme1n1` and `nvme0n1`):

1.  **Open `parted` for the Disk:**

    ```bash
    bashCopy codeparted /dev/nvme1n1
    ```
2.  **Print the Current Partition Table:** In the `parted` prompt, type:

    ```bash
    bashCopy codeprint
    ```
3.  **Resize the Partition (`p3`):**

    ```bash
    bashCopy coderesizepart 3 100%
    ```

    This resizes the third partition to use all remaining space on the disk. Type `Yes` if prompted for confirmation.
4.  **Exit `parted`:**

    ```bash
    bashCopy codequit
    ```

Repeat these steps for the second disk (`nvme0n1`):

```bash
bashCopy codeparted /dev/nvme0n1
```

Follow the same commands to resize `p3` on this disk.

#### **Step 5: Expand the ZFS Pool**

Run the following command to grow the `rpool` and make it use the newly resized partitions:

```bash
bashCopy codezpool online -e rpool nvme-eui.ace42e003554b1072ee4ac0000000001-part3
zpool online -e rpool nvme-eui.0000000624098476caf25b0320000086-part3
```

#### **Step 6: Verify the Expansion**

After running the above commands, check the pool's status to confirm the expanded capacity:

```bash
bashCopy codezpool list
```

Share the output of `zpool list` to verify the expansion.

4o

**You said:**

NAME SIZE ALLOC FREE CKPOINT EXPANDSZ FRAG CAP DEDUP HEALTH ALTROOT rpool 4.65T 2.15G 4.65T - - 0% 0% 1.00x ONLINE -

**ChatGPT said:**

ChatGPT

Excellent! Your ZFS pool (`rpool`) has been successfully expanded to utilize the full capacity of both disks, now showing **4.65 TB total size** with plenty of free space.
