---
title: Offloading domain TTY output to console with custom kernel/initramfs images  
subsection: virtualization  
order: 12  
---

# Offloading domain TTY output to console with custom kernel/initramfs images

1. Navigate to the `/boot` directory of the Fedora installation of the host to grab some kernel and initramfs images.  
   ```
   cd /boot && ls -l
   ```
   The following is an example output for the above command.  
   ```
   total 239596
   -rw-r--r--. 1 root root   234567 Jul 21 02:13 config-5.13.4-200.fc34.x86_64
   -rw-r--r--. 1 root root   234567 Jul 25 22:05 config-5.13.5-200.fc34.x86_64
   -rw-r--r--. 1 root root   234567 Jul 28 21:17 config-5.13.6-200.fc34.x86_64
   drwx------. 4 root root     4096 Jan  1  1970 efi
   -rw-r--r--. 1 root root   155544 Jan 27  2021 elf-memtest86+-5.31
   drwxr-xr-x. 2 root root     4096 Apr 23 16:26 extlinux
   drwx------. 2 root root     4096 Aug  2 13:07 grub2
   -rw-------. 1 root root 84860404 Jul 12 00:09 initramfs-0-rescue-8ee701c92f0f486cbb7afe96e5b7ea67.img
   -rw-------. 1 root root 33023557 Jul 23 18:49 initramfs-5.13.4-200.fc34.x86_64.img
   -rw-------. 1 root root 33002599 Jul 30 08:37 initramfs-5.13.5-200.fc34.x86_64.img
   -rw-------. 1 root root 32910001 Aug  2 14:44 initramfs-5.13.6-200.fc34.x86_64.img
   drwxr-xr-x. 3 root root     4096 Jul 12 00:09 loader
   drwx------. 2 root root    16384 Jul 12 00:06 lost+found
   -rw-r--r--. 1 root root   153868 Jan 27  2021 memtest86+-5.31
   -rw-------. 1 root root  5778689 Jul 21 02:13 System.map-5.13.4-200.fc34.x86_64
   -rw-------. 1 root root  5778727 Jul 25 22:05 System.map-5.13.5-200.fc34.x86_64
   -rw-------. 1 root root  5778835 Jul 28 21:17 System.map-5.13.6-200.fc34.x86_64
   -rwxr-xr-x. 1 root root 10580240 Jul 12 00:09 vmlinuz-0-rescue-8ee701c92f0f486cbb7afe96e5b7ea67
   -rwxr-xr-x. 1 root root 10853744 Jul 21 02:13 vmlinuz-5.13.4-200.fc34.x86_64
   -rwxr-xr-x. 1 root root 10851312 Jul 25 22:05 vmlinuz-5.13.5-200.fc34.x86_64
   -rwxr-xr-x. 1 root root 10850800 Jul 28 21:17 vmlinuz-5.13.6-200.fc34.x86_64
   ```
2. With appropriate permissions, copy the kernel images to a reference directory `linxkrnl` and the initramfs images to a reference directory `initrmfs`.  
   ```
   sudo cp /boot/vmlinux-* linxkrnl/
   ```
   ```
   sudo cp /boot/initramfs-* initrmfs/
   ```
3. Take up the ownership of the copied kernel images and kernel images by executing the following command on the reference directories `linxkrnl` and `initrmfs` respectively.  
   ```
   sudo chown $(whoami):$(whoami) linxkrnl/ --recursive
   ```
   ```
   sudo chown $(whoami):$(whoami) initrmfs/ --recursive
   ```
   ```
   ls -l linxkrnl/
   ```
   The following is an example output for the above command.  
   ```
   total 42136
   -rwxr-xr-x. 1 t0xic0der t0xic0der 10580240 Aug  2 15:35 vmlinuz-0-rescue-8ee701c92f0f486cbb7afe96e5b7ea67
   -rwxr-xr-x. 1 t0xic0der t0xic0der 10853744 Aug  2 15:35 vmlinuz-5.13.4-200.fc34.x86_64
   -rwxr-xr-x. 1 t0xic0der t0xic0der 10851312 Aug  2 15:35 vmlinuz-5.13.5-200.fc34.x86_64
   -rwxr-xr-x. 1 t0xic0der t0xic0der 10850800 Aug  2 15:35 vmlinuz-5.13.6-200.fc34.x86_64
   ```
   ```
   ls -l initrmfs/
   ```
   The following is an example output for the above command.  
   ```
   total 179496
   -rw-------. 1 t0xic0der t0xic0der 84860404 Aug  2 15:36 initramfs-0-rescue-8ee701c92f0f486cbb7afe96e5b7ea67.img
   -rw-------. 1 t0xic0der t0xic0der 33023557 Aug  2 15:36 initramfs-5.13.4-200.fc34.x86_64.img
   -rw-------. 1 t0xic0der t0xic0der 33002599 Aug  2 15:36 initramfs-5.13.5-200.fc34.x86_64.img
   -rw-------. 1 t0xic0der t0xic0der 32910001 Aug  2 15:36 initramfs-5.13.6-200.fc34.x86_64.img
   ```
4. Reuse the domain with the custom partitioning based on EXT4  that was created by the end of the **Setting up Fedora Workstation VM on QEMU using BIOS** and start it up by executing the following command.  
   ```
   qemu-system-x86_64 \
     -boot menu=on \
     -m 2048 \
     -cpu max \
     -smp 4 \
     -drive file=datadrct/fedobios.raw,format=raw \
     -accel kvm
   ```
5. In a new terminal session inside the virtualized domain, execute the following command to fetch the parameters passed to the kernel during boot.  
   ```
   cat /proc/cmdline
   ```
   The following is an example output for the above command.  
   ```
   BOOT_IMAGE=(hd0,msdos1)/vmlinuz-5.11.12-300.fc34.x86_64 root=UUID=0fa356e9-9509-4e18-8283-8983254c79d1 ro rhgb quiet
   ```
   Take a note of the UUID for the root partition and the same can be confirmed by executing the following command in a terminal session inside the virtualized domain.  
   ```
   cat /etc/fstab
   ```
   The following is an example output for the above command.
   ```
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
6. Power off the virtualized domain and start it up again by executing the following command with the correct UUID for the root partition.  
   ```
   qemu-system-x86_64 \
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
7. A lot of `systemd` prompts would show up on the console and the virtualized domain would boot up. The following is an example output for the above command.  
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
   
   fedorable login: t0xic0der
   Password: 
   Last login: Tue Aug  3 09:31:12 on tty2
   [t0xic0der@fedorable ~]$
   ```
8. As the kernel image and initramfs image versions that we used here are dissimilar from the version of the firmware installed on the virtualized domain, there can be kernel modules which are broken or incompletely loaded.  
   ```
   ip a
   ```
   ```
   1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
       link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
       inet 127.0.0.1/8 scope host lo
          valid_lft forever preferred_lft forever
       inet6 ::1/128 scope host 
          valid_lft forever preferred_lft forever
   ```
   As evidenced by the output of the above command executed inside the console of the virtualized domain, the kernel modules for network are apparently broken and the hostname of the host is taken up by the virtualized domain due to the mismatch of kernel images, initramfs images and installed firmware versions.  
9. For best compatibility, keep the versions for kernel image, initramfs image and installed firmware inline with each other. Instructions for the same have been provided in the **Offloading domain TTY output to console with original kernel/initramfs images** documentation.  
