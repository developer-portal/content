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
2. Source OVMF UEFI assets by following the [**Fetching OVMF UEFI from the correct source**](/tools/virtualization/fetching-ovmf-uefi-from-the-correct-source.html) guide, if not done already.  
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
   ![01](/content/tools/virtualization/images/setting-viewport-resolution-using-ovmf-bios/01.png)
5. Once inside the OVMF UEFI settings, just use the arrow keys to point at `Continue` and press `ENTER` to resume booting.  
   ![02](/content/tools/virtualization/images/setting-viewport-resolution-using-ovmf-bios/02.png)
6. QEMU would now boot into the live environment of Fedora Workstation so use the arrow keys to point at the first option and press `ENTER` to boot up.  
   ![03](/content/tools/virtualization/images/setting-viewport-resolution-using-ovmf-bios/03.png)
7. Once the live environment of Fedora Workstation has booted up, open up a terminal instance.  
   ![04](/content/tools/virtualization/images/setting-viewport-resolution-using-ovmf-bios/04.png)
8. Execute the following command to install `xrandr` on the live environment.  
   ```console
   $ sudo dnf install xrandr
   ```
9. Once `xrandr` is installed on the live environment, execute it to find a list of supported resolutions and refresh rates for the current renderer.  
   ```console
   $ xrandr
   ```
   ![05](/content/tools/virtualization/images/setting-viewport-resolution-using-ovmf-bios/05.png)
10. Restart the live environment and press the `ESC` key during the startup to navigate into the OVMF UEFI settings.  
    ![06](/content/tools/virtualization/images/setting-viewport-resolution-using-ovmf-bios/06.png)
11. Use the arrow keys to point at `Device Manager`, press `ENTER` and then select the `OVMF Platform Configuration` option.  
    ![07](/content/tools/virtualization/images/setting-viewport-resolution-using-ovmf-bios/07.png)
12. Observe that the `Preferred Resolution at Next Boot` is `UNSET`. Open up the popup for `Change Preferred Resolution for Next Boot` and select `1280x720`.  
    ![08](/content/tools/virtualization/images/setting-viewport-resolution-using-ovmf-bios/08.png)
13. Press `F10` key and then press `Y` to confirm saving the configuration. Press `Ctrl` + `Alt` + `Del` to reboot the VM.  
    ![09](/content/tools/virtualization/images/setting-viewport-resolution-using-ovmf-bios/09.png)
14. Once the booting into the live environment, the set resolution would be made available to select from the list of all other resolution.  
