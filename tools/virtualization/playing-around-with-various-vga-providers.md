---
title: Playing around with various VGA providers  
subsection: virtualization  
order: 11  
---

# Playing around with various VGA providers

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
      ![01](/content/tools/virtualization/images/playing-around-with-various-vga-providers/01.png)
   2. `lspci`  
      ![02](/content/tools/virtualization/images/playing-around-with-various-vga-providers/02.png)
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
   ![03](/content/tools/virtualization/images/playing-around-with-various-vga-providers/03.png)
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
      ![04](/content/tools/virtualization/images/playing-around-with-various-vga-providers/04.png)
   2. `lspci`  
      ![05](/content/tools/virtualization/images/playing-around-with-various-vga-providers/05.png)
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
      ![06](/content/tools/virtualization/images/playing-around-with-various-vga-providers/06.png)
   2. `lspci`  
      ![07](/content/tools/virtualization/images/playing-around-with-various-vga-providers/07.png)
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
   ![08](/content/tools/virtualization/images/playing-around-with-various-vga-providers/08.png)
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
      ![09](/content/tools/virtualization/images/playing-around-with-various-vga-providers/09.png)
   2. `lspci`  
      ![10](/content/tools/virtualization/images/playing-around-with-various-vga-providers/10.png)
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
      ![11](/content/tools/virtualization/images/playing-around-with-various-vga-providers/11.png)
   2. `lspci`  
      ![12](/content/tools/virtualization/images/playing-around-with-various-vga-providers/12.png)

## References
1. [https://www.kraxel.org/blog/2019/09/display-devices-in-qemu/](https://www.kraxel.org/blog/2019/09/display-devices-in-qemu/)
