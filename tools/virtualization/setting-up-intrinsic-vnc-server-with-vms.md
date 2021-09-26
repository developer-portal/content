---
title: Setting up intrinsic VNC server with VMs  
subsection: virtualization  
order: 6  
---

# Setting up intrinsic VNC server with VMs

> More information can be found here https://qemu-project.gitlab.io/qemu/system/vnc-security.html

1. Download the Fedora Workstation ISO file from website and store it in a reference directory `cdromimg`.  
   ```
   https://getfedora.org
   ```
2. Start a virtual machine for setting up intrinsic VNC server for the live ISO and there is no need for a virtual disk image here.  
   ```console
   $ qemu-system-x86_64 \
       -boot menu=on \
       -m 2048 \
       -cpu max \
       -smp 4 \
       -cdrom cdromimg/<Fedora-Workstation-Live-x86_64-xx-y.z.iso> \
       -vnc 0.0.0.0:59,password=on \
       -accel kvm
       -monitor stdio
   ```
   ```
   QEMU 5.2.0 monitor - type 'help' for more information
   (qemu) 
   ```
3. Visit https://www.realvnc.com/en/connect/download/viewer/ in an internet browser of choice, download and install the VNC viewer application either on the host device or another device in the same network.  
4. Head back to the prompt where the VM was started and type in the following command in the `(qemu)` console to change the default VNC password.  
   ```
   change vnc password
   ```
   ```
   QEMU 5.2.0 monitor - type 'help' for more information
   (qemu) change vnc password
   Password: ********
   ```
5. Switch to the VNC Viewer window and type in `0.0.0.0:5959` from the host device (or `<ip-address-of-host-device>:5959` if accessed from another device in the same network) - `59` from the command referring to the offset from `5900` which is the default VNC port.  
   ![01](https://user-images.githubusercontent.com/49605954/127031511-21e8853d-7d34-4192-9c46-f510f716e6ec.png)
6. A window would appear warning about the nature of the connection being unencrypted. This is fine for a closed network so click on the `Continue` button.  
   ![02](https://user-images.githubusercontent.com/49605954/127031516-97fc7f1f-2f66-4aea-9a51-2704cd4d130d.png)
7. Another window would appear which would ask for password. Enter the password that was set in the step #5 and then click on the `OK` button.  
   ![03](https://user-images.githubusercontent.com/49605954/127031519-117036dc-c8a6-41f8-af28-8bafd368017b.png)
8. Finally a window showing the virtual desktop of the live environment would show up and it can be used to interact with the VM.  
   ![04](https://user-images.githubusercontent.com/49605954/127031520-47639fc8-e38c-4448-92f1-44a6cb99a2e6.png)
