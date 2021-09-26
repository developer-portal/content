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
   ![01](https://user-images.githubusercontent.com/49605954/127776674-b4d8b61f-1fc1-41f8-95db-4cc0d607f194.png)  
   ![02](https://user-images.githubusercontent.com/49605954/127780377-4999ee0c-a256-42d7-99b2-9b791f31f26e.png)  
5. A greeting window would open up, providing with two options - Either to `Try Fedora` or `Install to Hard Drive`.  
   Close the window for now.  
   ![03](https://user-images.githubusercontent.com/49605954/127777826-749920ab-06d1-4a8a-99a7-0955a5dd69fa.png)  
6. In a new terminal session inside the virtualized guest, execute the following command to confirm UEFI boot.  
   ```console
   $ ls -la /sys/firmware/efi/efivars/
   ```
   ![04](https://user-images.githubusercontent.com/49605954/127778019-b6bee93c-da46-4bed-b6f3-81b6b2029252.png)  
7. Open up the installer application by clicking on the `Install to Hard Drive` icon from the GNOME drawer inside the virtualized guest.  
   ![05](https://user-images.githubusercontent.com/49605954/127778125-78c8c2cb-f2d4-4134-87e3-694411823e57.png)  
8. Pick the language of choice to proceed with the installation on the installer application.  
   ![06](https://user-images.githubusercontent.com/49605954/127777697-5903dac7-2ca4-4fca-8bc8-39718f62412c.png)  
9. Configure the installation to liking and then click on `Begin Installation` on the installer application to start.  
   ![07](https://user-images.githubusercontent.com/49605954/127777923-69d0dd4d-f920-4363-9480-52d0bbe9cddb.png)  
   1. BTRFS partitioning is recommended and the partitioning scheme is configured to be considered as a default. Proceed with the automatic partitioning scheme as illustrated in the following screenshot to apply the recommended partitioning.  
      ![08](https://user-images.githubusercontent.com/49605954/127862027-95e55141-cdc4-4bad-8490-cece5f6810f2.png)  
   2. In case of a requirement of a custom partitioning scheme, toggle the `Custom` radio button under `Storage Configuration` and click on `Done` button to move to the page where custom partitioning scheme can be selected.  
      ![09](https://user-images.githubusercontent.com/49605954/127862601-e126c7ed-ffd8-4aba-8755-4fac2aa9f0d5.png)  
      For the sake of simplicity, the partitions are configured in the following manner.  
      
      | Partition | Desired Capacity | File System            | Mount Point | Device Type        | Reformat? | Encrypt? |
      |-----------|------------------|------------------------|-------------|--------------------|-----------|----------|
      | /dev/sda1 | 1GiB             | EFI Standard Partition | /boot/efi   | Standard Partition | Yes       | No       |
      | /dev/sda2 | 15GiB            | EXT4                   | /           | Standard Partition | Yes       | No       |
      
      ![10](https://user-images.githubusercontent.com/49605954/127863184-98799d31-9346-497b-884a-198df9e42efd.png)  
10. Let the installation finish, click the `Finish Installation` button to exit the installer application and then power off the virtualized guest.  
    ![11](https://user-images.githubusercontent.com/49605954/127864129-67d1884a-cdbc-4471-803f-97b43d4f03ac.png)  
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
    ![12](https://user-images.githubusercontent.com/49605954/127778478-84669816-87c4-4c39-a702-b07fd6f3f9c7.png)  
