---
title: Setting up Fedora Workstation VM on QEMU using UEFI  
subsection: virtualization  
order: 5  
---

# Setting up Fedora Workstation VM on QEMU using UEFI

1. Download the Fedora Workstation ISO file from website and store it in a reference directory `cdromimg`.  
   ```
   https://getfedora.org
   ```
2. Source OVMF UEFI assets by following the **Fetching OVMF UEFI from the correct source** guide, if not done already.  
3. Create a virtual disk image of type `16GB` and of format `RAW` in a reference directory `datadrct` by executing the following command.  
   ```console
   $ qemu-img create -f raw datadrct/fedouefi.raw 16G
   ```
4. Start a virtual machine for installing Fedora Workstation on the virtual disk image by executing the following command on the host.  
   ```console
   $ qemu-system-x86_64 \
       -boot menu=on \
       -m 2048 \
       -cpu max \
       -smp 4 \
       -cdrom cdromimg/<Fedora-Workstation-Live-x86_64-xx-y.z.iso> \
       -drive file=datadrct/fedouefi.raw,format=raw \
       -bios /usr/share/edk2/ovmf/OVMF_CODE.fd \
       -accel kvm
   ```
   ![01](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-uefi/01.png)  
   ![02](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-uefi/02.png)  
5. A greeting window would open up, providing with two options - Either to `Try Fedora` or `Install to Hard Drive`.  
   Close the window for now.  
   ![03](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-uefi/03.png)  
6. In a new terminal session inside the virtualized guest, execute the following command to confirm UEFI boot.  
   ```console
   $ ls -la /sys/firmware/efi/efivars/
   ```
   ![04](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-uefi/04.png)  
7. Open up the installer application by clicking on the `Install to Hard Drive` icon from the GNOME drawer inside the virtualized guest.  
   ![05](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-uefi/05.png)  
8. Pick the language of choice to proceed with the installation on the installer application.  
   ![06](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-uefi/06.png)  
9. Configure the installation to liking and then click on `Begin Installation` on the installer application to start.  
   ![07](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-uefi/07.png)  
   1. BTRFS partitioning is recommended and the partitioning scheme is configured to be considered as a default. Proceed with the automatic partitioning scheme as illustrated in the following screenshot to apply the recommended partitioning.  
      ![08](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-uefi/08.png)  
   2. In case of a requirement of a custom partitioning scheme, toggle the `Custom` radio button under `Storage Configuration` and click on `Done` button to move to the page where custom partitioning scheme can be selected.  
      ![09](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-uefi/09.png)  
      For the sake of simplicity, the partitions are configured in the following manner.  
      
      | Partition | Desired Capacity | File System            | Mount Point | Device Type        | Reformat? | Encrypt? |
      |-----------|------------------|------------------------|-------------|--------------------|-----------|----------|
      | /dev/sda1 | 1GiB             | EFI Standard Partition | /boot/efi   | Standard Partition | Yes       | No       |
      | /dev/sda2 | 15GiB            | EXT4                   | /           | Standard Partition | Yes       | No       |
      
      ![10](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-uefi/10.png)  
10. Let the installation finish, click the `Finish Installation` button to exit the installer application and then power off the virtualized guest.  
    ![11](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-uefi/11.png)  
11. Start a virtual machine where Fedora Workstation was just installed by executing the following command on the host.  
    ```console
    $ qemu-system-x86_64 \
        -boot menu=on \
        -m 2048 \
        -cpu max \
        -smp 4 \
        -drive file=datadrct/fedouefi.raw,format=raw \
        -bios /usr/share/edk2/ovmf/OVMF_CODE.fd \
        -accel kvm
    ```
12. Set up the Fedora Workstation according to preferences.  
    ![12](/content/tools/virtualization/images/setting-up-fedora-workstation-vm-on-qemu-using-uefi/12.png)  
