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
   ```
   qemu-img create -f raw datadrct/fedobios.raw 16G
   ```
3. Start a virtual machine for installing Fedora Workstation on the virtual disk image by executing the following command on the host.  
   ```
   qemu-system-x86_64 \
     -boot menu=on \
     -m 2048 \
     -cpu max \
     -smp 4 \
     -cdrom cdromimg/<Fedora-Workstation-Live-x86_64-xx-y.z.iso> \
     -drive file=datadrct/fedobios.raw,format=raw \
     -accel kvm
   ```
   ![01](https://user-images.githubusercontent.com/49605954/127779866-996b592d-ffdd-4ba4-bf5a-b5b8d777faf8.png)  
   ![02](https://user-images.githubusercontent.com/49605954/127779891-00e39b94-94c4-45cf-b40c-64d95149d154.png)  
4. A greeting window would open up, providing with two options - Either to `Try Fedora` or `Install to Hard Drive`.  
   Click on the `Install to Hard Drive` button to open up the installer application.  
   ![03](https://user-images.githubusercontent.com/49605954/127779998-9cce4f95-7b7f-488a-804d-b198830f9830.png)  
5. Pick the language of choice to proceed with the installation on the installer application.  
   ![04](https://user-images.githubusercontent.com/49605954/127780073-8cc948fe-048e-4796-ba0b-474711cd93d0.png)  
6. Configure the installation to liking and then click on `Begin Installation` on the installer application to start.  
   ![05](https://user-images.githubusercontent.com/49605954/127780144-bcf1788b-d223-49c3-b8d9-97500e57071c.png)  
   1. BTRFS partitioning is recommended and the partitioning scheme is configured to consider it as a default. Proceed with the automatic partitioning scheme as illustrated in the following screenshot to apply the recommended partitioning.  
      ![06](https://user-images.githubusercontent.com/49605954/127868344-a55eaf9d-ea90-4325-b37f-af00654996db.png)  
   2. In case of a requirement of a custom partitioning scheme, toggle the `Custom` radio button under `Storage Configuration` and click on `Done` button to move to the page where custom partitioning scheme can be selected.  
      ![07](https://user-images.githubusercontent.com/49605954/127868214-1bbb5687-b041-49d0-a3d4-5e42b300eed9.png)  
      For the sake of simplicity, the partitions are configured in the following manner.  
      
      | Partition | Desired Capacity | File System            | Mount Point | Device Type        | Reformat? | Encrypt? |
      |-----------|------------------|------------------------|-------------|--------------------|-----------|----------|
      | /dev/sda1 | 1GiB             | EXT4                   | /boot       | Standard Partition | Yes       | No       |
      | /dev/sda2 | 15GiB            | EXT4                   | /           | Standard Partition | Yes       | No       |
      
      ![08](https://user-images.githubusercontent.com/49605954/127868564-3bcadc38-58e9-442c-b0d6-e1a31d2dfc06.png)  
7. Let the installation finish, click the `Finish Installation` button to exit the installer application and then power off the virtualized guest.  
   ![09](https://user-images.githubusercontent.com/49605954/127864129-67d1884a-cdbc-4471-803f-97b43d4f03ac.png)  
8. Start a virtual machine where Fedora Workstation was just installed by executing the following command on the host.  
    ```
    qemu-system-x86_64 \
      -boot menu=on \
      -m 2048 \
      -cpu max \
      -smp 4 \
      -drive file=datadrct/fedobios.raw,format=raw \
      -accel kvm
    ```
9. Set up the Fedora Workstation according to preferences.  
    ![10](https://user-images.githubusercontent.com/49605954/127778478-84669816-87c4-4c39-a702-b07fd6f3f9c7.png)  
