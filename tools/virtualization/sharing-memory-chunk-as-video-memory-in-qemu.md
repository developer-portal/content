---
title: Sharing a chunk of memory as video memory in QEMU  
subsection: virtualization  
order: 9  
---

# Sharing a chunk of memory as video memory in QEMU

1. Continuing on from the end of the guide about [**Setting up Fedora Workstation VM on QEMU using BIOS**](/tools/virtualization/setting-up-fedora-workstation-vm-on-qemu-using-bios.html), start up the same VM by executing the following command.  
   ```console
   $ qemu-system-x86_64 \
       -boot menu=on \
       -m 2048 \
       -cpu max \
       -smp 4 \
       -drive file=datadrct/fedobios.raw,format=raw \
       -accel kvm \
       -vga std \
       -device VGA,vgamem_mb=512
   ```
2. Execute the following command inside the console of the VM to view the list of the emulated PCI hardware attached.  
   ```console
   $ lspci
   00:00.0 Host bridge: Intel Corporation 440FX - 82441FX PMC [Natoma] (rev 02)
   00:01.0 ISA bridge: Intel Corporation 82371SB PIIX3 ISA [Natoma/Triton II]
   00:01.1 IDE interface: Intel Corporation 82371SB PIIX3 IDE [Natoma/Triton II]
   00:01.3 Bridge: Intel Corporation 82371AB/EB/MB PIIX4 ACPI (rev 03)
   00:02.0 VGA compatible controller: Device 1234:1111 (rev 02)
   00:03.0 Ethernet controller: Intel Corporation 82540EM Gigabit Ethernet Controller (rev 03)
   ```
3. Probe into the output of `00:02.0` by executing the following command as it seems to be an emulated VGA controller.  
   ```console
   $ lspci -v -s 00:02.0
   00:02.0 VGA compatible controller: Device 1234:1111 (rev 02) (prog-if 00 [VGA controller])
           Subsystem: Red Hat, Inc. Device 1100
           Flags: fast devsel
           Memory at fd000000 (32-bit, prefetchable) [size=512M]
           Memory at febf0000 (32-bit, non-prefetchable) [size=4K]
           Expansion ROM at 000c0000 [disabled] [size=128K]
           Kernel driver in use: bochs-drm
           Kernel modules: bochs_drm
   ```
4. There are many providers like `qxl`, `virtio`, `vmware` etc. that can be used in place of `std`.  
