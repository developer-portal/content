---
title: Setting up Fedora Workstation VM on QEMU using BIOS  
subsection: virtualization  
order: 4  
---

# Setting up Fedora Workstation VM on QEMU using BIOS

1. Download the Fedora Workstation ISO file from website and store it in a reference directory `cdromimg`.  
   ```
   https://getfedora.org
   ```
2. Create a virtual disk image of type `16GB` and of format `RAW` in a reference directory `datadrct` by executing the following command.  
   ```console
   $ qemu-img create -f raw datadrct/fedobios.raw 16G
   ```
3. Start a virtual machine for installing Fedora Workstation on the virtual disk image by executing the following command on the host.  
   ```console
   $ qemu-system-x86_64 \
       -boot menu=on \
       -m 2048 \
       -cpu max \
       -smp 4 \
       -cdrom cdromimg/<Fedora-Workstation-Live-x86_64-xx-y.z.iso> \
       -drive file=datadrct/fedobios.raw,format=raw \
       -accel kvm
   ```
   ![01](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-bios/01.png)  
   ![02](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-bios/02.png)  
4. A greeting window would open up, providing with two options - Either to `Try Fedora` or `Install to Hard Drive`.  
   Click on the `Install to Hard Drive` button to open up the installer application.  
   ![03](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-bios/03.png)  
5. Pick the language of choice to proceed with the installation on the installer application.  
   ![04](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-bios/04.png)  
6. Configure the installation to liking and then click on `Begin Installation` on the installer application to start.  
   ![05](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-bios/05.png)  
   1. BTRFS partitioning is recommended and the partitioning scheme is configured to consider it as a default. Proceed with the automatic partitioning scheme as illustrated in the following screenshot to apply the recommended partitioning.  
      ![06](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-bios/06.png)  
   2. In case of a requirement of a custom partitioning scheme, toggle the `Custom` radio button under `Storage Configuration` and click on `Done` button to move to the page where custom partitioning scheme can be selected.  
      ![07](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-bios/07.png)  
      For the sake of simplicity, the partitions are configured in the following manner.  
      
      | Partition | Desired Capacity | File System            | Mount Point | Device Type        | Reformat? | Encrypt? |
      |-----------|------------------|------------------------|-------------|--------------------|-----------|----------|
      | /dev/sda1 | 1GiB             | EXT4                   | /boot       | Standard Partition | Yes       | No       |
      | /dev/sda2 | 15GiB            | EXT4                   | /           | Standard Partition | Yes       | No       |
      
      ![08](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-bios/08.png)  
7. Let the installation finish, click the `Finish Installation` button to exit the installer application and then power off the virtualized guest.  
   ![09](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-bios/09.png)  
8. Start a virtual machine where Fedora Workstation was just installed by executing the following command on the host.  
    ```console
    $ qemu-system-x86_64 \
        -boot menu=on \
        -m 2048 \
        -cpu max \
        -smp 4 \
        -drive file=datadrct/fedobios.raw,format=raw \
        -accel kvm
    ```
9. Set up the Fedora Workstation according to preferences.  
    ![10](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-bios/10.png)  
