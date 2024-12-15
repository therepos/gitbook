# Test : GPU on LXC

To configure an LXC container to use the NVIDIA GPU installed on the Proxmox host, you'll need to follow these steps:

1.  Install the NVIDIA drivers and necessary tools on both the host and the container:

    *   On the Proxmox host:

        ```
        sudo apt-get update
        sudo apt-get install nvidia-driver-470 nvidia-container-toolkit nvidia-modprobe
        ```
    *   Inside the LXC container:

        ```
        lxc exec <container-name> -- sh -c "apt-get update"
        lxc exec <container-name> -- sh -c "apt-get install nvidia-driver-470 nvidia-container-toolkit nvidia-modprobe"
        ```

    Replace `<container-name>` with the name of your LXC container.
2.  Create or modify a new configuration file for your LXC container to enable GPU passthrough:

    *   Create or edit the following configuration file in the Proxmox host (e.g., `/etc/lxc/<container-name>.conf`):

        ```
        lcctool.enabled = 1
        lcctool.nvidia-device = all
        ```

    This configures LXC to use the NVIDIA Container Toolkit (`lcctool`) and enables GPU passthrough for all available devices.
3.  Restart the container with the updated configuration:

    ```
    lxc restart <container-name>
    ```
4.  Verify that the container can access the GPU:

    *   Inside the container, run the following command to list available GPUs:

        ```
        nvidia-smi
        ```

    If the container can access the GPU, you should see information about the device(s) displayed in the terminal.

By completing these steps, your LXC container should now be able to utilize the NVIDIA GPU installed on the Proxmox host. Keep in mind that this configuration may require adjustments for different versions of drivers and containers, so it's essential to consult the relevant documentation for your specific setup if you encounter any issues.
