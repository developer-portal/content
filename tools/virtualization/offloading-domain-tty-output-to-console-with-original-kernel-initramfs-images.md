---
title: Offloading domain TTY output to console with original kernel/initramfs images  
subsection: virtualization  
order: 13  
---

# Offloading domain TTY output to console with original kernel/initramfs images

> This documentation extends from the [**Offloading domain TTY output to console with custom kernel/initramfs images**](/tools/virtualization/offloading-domain-tty-output-to-console-with-custom-kernel-initramfs-images.html) documentation, so it is highly recommended to read that document first.

## Introduction

In a headless virtual machine hosts accessible by SSH, the activities on a virtual machines can be discovered by offloading the console prompts on the current TTY. This is a great alternative to setting up SSH inside the virtual machine or connecting to the virtual machine via VNC or SPICE.

## Steps

1. Reuse the domain with the custom partitioning based on EXT4  that was created by the end of the [**Setting up Fedora Workstation VM on QEMU using BIOS**](/tools/virtualization/setting-up-fedora-workstation-vm-on-qemu-using-bios.html) and start it up by executing the following command.  
   ```console
   $ qemu-system-x86_64 \
       -boot menu=on \
       -m 2048 \
       -cpu max \
       -smp 4 \
       -net nic \
       -net user,hostfwd=tcp::6969-:8080 \
       -drive file=datadrct/fedobios.raw,format=raw \
       -accel kvm
   ```
2. In a new terminal session of the virtualized domain, execute the following command to fetch details about the currently used kernel image version.  
   ```console
   $ uname -a
   ```
   ![01](/content/tools/virtualization/images/offloading-domain-tty-output-to-console-with-original-kernel-initramfs-images/01.png)
3. With appropriate permissions, copy the kernel image and the initramfs image of the aforementioned version to the home directory of the default user in the virtualized domain.  
   ```console
   $ ls -la /boot
   ```
   ![02](/content/tools/virtualization/images/offloading-domain-tty-output-to-console-with-original-kernel-initramfs-images/02.png)
   ```console
   $ sudo cp /boot/<vmlinux-x.yy.zz-aaa-fcRR.x86_64> .
   $ sudo cp /boot/<initramfs-x.yy.zz-aaa-fcRR.x86_64.img> .
   $ ls -lh .
   ```
   ![03](/content/tools/virtualization/images/offloading-domain-tty-output-to-console-with-original-kernel-initramfs-images/03.png)
4. Take up the ownership of the copied kernel images and kernel images by executing the following command in a terminal session in the virtualized domain.  
   ```console
   $ sudo chown $(whoami):$(whoami) <vmlinux-x.yy.zz-aaa-fcRR.x86_64>
   $ sudo chown $(whoami):$(whoami) <initramfs-x.yy.zz-aaa-fcRR.x86_64.img>
   $ ls -lh .
   ```
   ![04](/content/tools/virtualization/images/offloading-domain-tty-output-to-console-with-original-kernel-initramfs-images/04.png)
5. Start an HTTP server in the same directory by executing the following command in a terminal session in the virtualized domain.  
   ```console
   $ python3 -m http.server 8080
   ```
   ![05](/content/tools/virtualization/images/offloading-domain-tty-output-to-console-with-original-kernel-initramfs-images/05.png)
6. In a new terminal session of the host, execute the following command to pull the kernel image and initramfs image into reference directories `linxkrnl` and `initrmfs` respectively.  
   ```console
   $ wget http://localhost:6969/vmlinuz-x.yy.zz-aaa.fcRR.x86_64 -O linxkrnl/vmlinuz-x.yy.zz-aaa.fcRR.x86_64
   $ wget http://localhost:6969/initramfs-x.yy.zz-aaa.fcRR.x86_64.img -O initrmfs/initramfs-x.yy.zz-aaa.fcRR.x86_64.img
   $ ls -lh linxkrnl/
   total 52M
   -rwxr-xr-x. 1 t0xic0der t0xic0der 11M Aug  2 15:35 vmlinuz-0-rescue-8ee701c92f0f486cbb7afe96e5b7ea67
   -rw-rw-r--. 1 t0xic0der t0xic0der 11M Aug  3 10:38 vmlinuz-5.11.12-300.fc34.x86_64
   -rwxr-xr-x. 1 t0xic0der t0xic0der 11M Aug  2 15:35 vmlinuz-5.13.4-200.fc34.x86_64
   -rwxr-xr-x. 1 t0xic0der t0xic0der 11M Aug  2 15:35 vmlinuz-5.13.5-200.fc34.x86_64
   -rwxr-xr-x. 1 t0xic0der t0xic0der 11M Aug  2 15:35 vmlinuz-5.13.6-200.fc34.x86_64
   $ ls -lh initrmfs/
   total 204M
   -rw-------. 1 t0xic0der t0xic0der 81M Aug  2 15:36 initramfs-0-rescue-8ee701c92f0f486cbb7afe96e5b7ea67.img
   -rw-rw-r--. 1 t0xic0der t0xic0der 29M Aug  3 10:38 initramfs-5.11.12-300.fc34.x86_64.img
   -rw-------. 1 t0xic0der t0xic0der 32M Aug  2 15:36 initramfs-5.13.4-200.fc34.x86_64.img
   -rw-------. 1 t0xic0der t0xic0der 32M Aug  2 15:36 initramfs-5.13.5-200.fc34.x86_64.img
   -rw-------. 1 t0xic0der t0xic0der 32M Aug  2 15:36 initramfs-5.13.6-200.fc34.x86_64.img
   ```
7. Execute the following command to fetch the parameters passed to the kernel during boot in a terminal session in the virtualized domain.  
   ```console
   $ cat /proc/cmdline
   BOOT_IMAGE=(hd0,msdos1)/vmlinuz-5.11.12-300.fc34.x86_64 root=UUID=0fa356e9-9509-4e18-8283-8983254c79d1 ro rhgb quiet
   ```
   Take a note of the UUID for the root partition and the same can be confirmed by executing the following command in a terminal session inside the virtualized domain.  
   ```console
   $ cat /etc/fstab
   #
   # /etc/fstab
   # Created by anaconda on Mon Aug  2 09:36:54 2021
   #
   # Accessible filesystems, by reference, are maintained under '/dev/disk/'.
   # See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info.
   #
   # After editing this file, run 'systemctl daemon-reload' to update systemd
   # units generated from this file.
   #
   UUID=0fa356e9-9509-4e18-8283-8983254c79d1 /                       ext4    defaults        1 1
   UUID=2d2863bb-527b-4477-bae5-5955bdb44d7b /boot                   ext4    defaults        1 2
   ```
8. Power off the virtualized domain and start it up again by executing the following command with the correct UUID for the root partition, correct names for kernel image and initramfs image which were recently fetched.  
   ```console
   $ qemu-system-x86_64 \
       -boot menu=on \
       -m 2048 \
       -cpu max \
       -smp 4 \
       -drive file=datadrct/fedobios.raw,format=raw \
       -accel kvm \
       -nographic \
       -kernel linxkrnl/<vmlinuz-x.yy.zz-aaa.fcRR.x86_64> \
       -initrd initrmfs/<initramfs-x.yy.zz-aaa.fcRR.x86_64.img> \
       -append "root=UUID=<xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx> rw console=ttyS0"
   ```
9. A lot of `systemd` prompts would show up on the console and the virtualized domain would boot up. The following is an example output for the above command.  
   ```
   ...
   [  OK  ] Started Network Manager Script Dispatcher Service.
   [  OK  ] Finished Network Manager Wait Online.
   [  OK  ] Reached target Network is Online.
   [  OK  ] Reached target Remote File Systems (Pre).
   [  OK  ] Reached target Remote File Systems.
            Starting Virtualization daemon...
            Starting Notify NFS peers of a restart...
            Starting Permit User Sessions...
   [  OK  ] Started Notify NFS peers of a restart.
   [  OK  ] Finished Permit User Sessions.
            Starting GNOME Display Manager...
            Starting Hold until boot process finishes up...
   [  OK  ] Started GNOME Display Manager.
   
   Fedora 34 (Workstation Edition)
   Kernel 5.13.6-200.fc34.x86_64 on an x86_64 (ttyS0)
   
   fedora login: t0xic0der
   Password: 
   Last login: Tue Aug  3 10:31:46 on tty2
   [t0xic0der@fedora ~]$
   ```
10. As the kernel image and initramfs image versions that we used here are similar to the version of the firmware installed on the virtualized domain, there can be kernel modules work just fine.  
    ```console
    $ ip a
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
        inet 127.0.0.1/8 scope host lo
           valid_lft forever preferred_lft forever
        inet6 ::1/128 scope host 
           valid_lft forever preferred_lft forever
    2: ens3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
        link/ether 52:54:00:12:34:56 brd ff:ff:ff:ff:ff:ff
        altname enp0s3
        inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute ens3
           valid_lft 86298sec preferred_lft 86298sec
        inet6 fec0::26ff:70eb:26b2:5923/64 scope site dynamic noprefixroute 
           valid_lft 86302sec preferred_lft 14302sec
        inet6 fe80::486a:c7b3:ca0a:43cf/64 scope link noprefixroute 
           valid_lft forever preferred_lft forever
    ```
    As evidenced by the output of the above command executed inside the console of the virtualized domain, the kernel modules for network now work just fine and the hostname of the virtualized host has been retained as the kernel images, initramfs images and installed firmware versions correspond with each other.  
