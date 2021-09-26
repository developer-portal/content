---
title: Playing around with various VGA providers  
subsection: virtualization  
order: 11  
---

# Playing around with various VGA providers

> More information can be found here https://www.kraxel.org/blog/2019/09/display-devices-in-qemu/

1. Download the Fedora Workstation ISO file from website and store it in a reference directory `cdromimg`.  
   ```
   https://getfedora.org
   ```
2. Execute the following command to know about the VGA providers available at disposal.  
   ```console
   $ qemu-system-x86_64 -vga help
   none                 no graphic card
   std                  standard VGA (default)
   cirrus               Cirrus VGA
   vmware               VMWare SVGA
   xenfb                Xen paravirtualized framebuffer
   qxl                  QXL VGA
   virtio               Virtio VGA
   ```
3. Start a virtual machine for playing around with various VGA providers for the live ISO and there is no need for a virtual disk image here.  
   ```console
   $ qemu-system-x86_64 \
       -boot menu=on \
       -m 8192 \
       -cpu max \
       -smp 4 \
       -cdrom cdromimg/<Fedora-Workstation-Live-x86_64-xx-y.z.iso> \
       -accel kvm
   ```
4. Open up `Settings` inside the VM and head over to the `About` section. Information about the `Graphics` can be seen here.  
5. Open up `Terminal` inside the VM and execute the `lspci` commands in regards with the current VGA controller to find more information on it.  

We will test out each VGA provider one-by-one and list the information for each now.  

1. Standard VGA (Default)  
   ```console
   $ qemu-system-x86_64 \
       -boot menu=on \
       -m 8192 \
       -cpu max \
       -smp 4 \
       -cdrom cdromimg/<Fedora-Workstation-Live-x86_64-xx-y.z.iso> \
       -accel kvm \
       -vga std
   ```
   1. `Settings` -> `About`  
      ![01](https://user-images.githubusercontent.com/49605954/127103479-b4eaddd3-ed03-4f81-aa28-1fc23ea56f8b.png)
   2. `lspci`  
      ![02](https://user-images.githubusercontent.com/49605954/127103484-f696d37d-b6c0-4b2b-b3df-6fb93ae1ada8.png)
2. No graphic card  
   ```console
   $ qemu-system-x86_64 \
       -boot menu=on \
       -m 8192 \
       -cpu max \
       -smp 4 \
       -cdrom cdromimg/<Fedora-Workstation-Live-x86_64-xx-y.z.iso> \
       -accel kvm \
       -vga none
   ```
   ![03](https://user-images.githubusercontent.com/49605954/127103486-578e5a86-d907-4c63-b91d-59eaf51e462f.png)
3. Cirrus VGA  
   ```console
   $ qemu-system-x86_64 \
       -boot menu=on \
       -m 8192 \
       -cpu max \
       -smp 4 \
       -cdrom cdromimg/<Fedora-Workstation-Live-x86_64-xx-y.z.iso> \
       -accel kvm \
       -vga cirrus
   ```
   1. `Settings` -> `About`  
      ![04](https://user-images.githubusercontent.com/49605954/127103490-a8888c09-7035-4259-8cb1-51f47d940f25.png)
   2. `lspci`  
      ![05](https://user-images.githubusercontent.com/49605954/127103492-aa8d3a74-14b8-4aa1-902d-46d1b4357824.png)
4. VMware SVGA  
   ```console
   $ qemu-system-x86_64 \
       -boot menu=on \
       -m 8192 \
       -cpu max \
       -smp 4 \
       -cdrom cdromimg/<Fedora-Workstation-Live-x86_64-xx-y.z.iso> \
       -accel kvm \
       -vga vmware
   ```
   1. `Settings` -> `About`  
      ![06](https://user-images.githubusercontent.com/49605954/127104339-f8e43975-2d98-4f1d-a3fd-4e3ce285ec15.png)
   2. `lspci`  
      ![07](https://user-images.githubusercontent.com/49605954/127104344-4629609b-cd34-4b7e-b359-792c73357020.png)
5. Xen paravirtualized framebuffer  
   ```console
   $ qemu-system-x86_64 \
       -boot menu=on \
       -m 8192 \
       -cpu max \
       -smp 4 \
       -cdrom cdromimg/<Fedora-Workstation-Live-x86_64-xx-y.z.iso> \
       -accel kvm \
       -vga xenfb
   ```
   ![08](https://user-images.githubusercontent.com/49605954/127104643-7b148366-deca-4695-beaa-781743e86c01.png)
6. QXL VGA  
   ```console
   $ qemu-system-x86_64 \
       -boot menu=on \
       -m 8192 \
       -cpu max \
       -smp 4 \
       -cdrom cdromimg/<Fedora-Workstation-Live-x86_64-xx-y.z.iso> \
       -accel kvm \
       -vga qxl
   ```
   1. `Settings` -> `About`  
      ![09](https://user-images.githubusercontent.com/49605954/127106060-279de080-83a4-4e17-97a0-cacddc6bb56c.png)
   2. `lspci`  
      ![10](https://user-images.githubusercontent.com/49605954/127106064-69a51398-326d-4e96-a220-c46cc37f22c5.png)
7. VirtIO VGA  
   ```console
   $ qemu-system-x86_64 \
       -boot menu=on \
       -m 8192 \
       -cpu max \
       -smp 4 \
       -cdrom cdromimg/<Fedora-Workstation-Live-x86_64-xx-y.z.iso> \
       -accel kvm \
       -vga virtio
   ```
   1. `Settings` -> `About`  
      ![11](https://user-images.githubusercontent.com/49605954/127106067-fb3217b3-e840-47cb-955b-6f9307524055.png)
   2. `lspci`  
      ![12](https://user-images.githubusercontent.com/49605954/127106070-632dbf75-320c-4537-a545-57fe1e999212.png)
