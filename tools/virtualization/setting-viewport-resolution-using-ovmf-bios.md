---
title: Setting viewport resolution using OVMF BIOS  
subsection: virtualization  
order: 7  
---

# Setting viewport resolution using OVMF BIOS

1. Download the Fedora Workstation ISO file from website and store it in a reference directory `cdromimg`.  
   ```
   https://getfedora.org
   ```
2. Source OVMF UEFI assets by following the **Fetching OVMF UEFI from the correct source** guide, if not done already.  
3. Start a virtual machine for playing around with setting viewport resolution for the live ISO and there is no need for a virtual disk image here.  
   ```console
   $ qemu-system-x86_64 \
       -boot menu=on \
       -m 2048 \
       -cpu max \
       -smp 4 \
       -bios /usr/share/edk2/ovmf/OVMF_CODE.fd \
       -cdrom cdromimg/<Fedora-Workstation-Live-x86_64-xx-y.z.iso> \
       -accel kvm
   ```
4. Press `ESC` key when the following screen is visible during the startup to navigate into the OVMF UEFI settings.  
   ![01](https://user-images.githubusercontent.com/49605954/127020743-854bfcf1-90f7-4a5c-8812-82dfc6c32d95.png)
5. Once inside the OVMF UEFI settings, just use the arrow keys to point at `Continue` and press `ENTER` to resume booting.  
   ![02](https://user-images.githubusercontent.com/49605954/127020748-04bd0470-5778-4acb-8c57-1217e61d1342.png)
6. QEMU would now boot into the live environment of Fedora Workstation so use the arrow keys to point at the first option and press `ENTER` to boot up.  
   ![03](https://user-images.githubusercontent.com/49605954/127020753-ba1ccb0e-6e0a-4a6d-9f73-a1ab60025ff5.png)
7. Once the live environment of Fedora Workstation has booted up, open up a terminal instance.  
   ![04](https://user-images.githubusercontent.com/49605954/127020756-6d9f7600-4ce7-4d7d-931d-31dd97295a02.png)
8. Execute the following command to install `xrandr` on the live environment.  
   ```console
   $ sudo dnf install xrandr
   ```
9. Once `xrandr` is installed on the live environment, execute it to find a list of supported resolutions and refresh rates for the current renderer.  
   ```console
   $ xrandr
   ```
   ![05](https://user-images.githubusercontent.com/49605954/127020760-402adde3-abcc-4648-a426-c4bac9b40983.png)
10. Restart the live environment and press the `ESC` key during the startup to navigate into the OVMF UEFI settings.  
    ![06](https://user-images.githubusercontent.com/49605954/127020761-2132247b-390b-4673-b367-779ebdb1b8a3.png)
11. Use the arrow keys to point at `Device Manager`, press `ENTER` and then select the `OVMF Platform Configuration` option.  
    ![07](https://user-images.githubusercontent.com/49605954/127020763-919c4f67-6ab1-4233-a1bb-8d310b90250b.png)
12. Observe that the `Preferred Resolution at Next Boot` is `UNSET`. Open up the popup for `Change Preferred Resolution for Next Boot` and select `1280x720`.  
    ![08](https://user-images.githubusercontent.com/49605954/127020765-73d234bf-4d45-47b6-91bf-df48e234d073.png)
13. Press `F10` key and then press `Y` to confirm saving the configuration. Press `Ctrl` + `Alt` + `Del` to reboot the VM.  
    ![09](https://user-images.githubusercontent.com/49605954/127020767-847dc3f4-4a50-422a-a606-92b9e3f60ccf.png)
14. Once the booting into the live environment, the set resolution would be made available to select from the list of all other resolution.  
