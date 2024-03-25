---
title: Fetching OVMF UEFI from the correct source  
subsection: virtualization  
order: 2  
---

# Fetching OVMF UEFI from the correct source

1. On the host device, execute either of the following commands to install OVMF, if not already installed.  
   1. **Stable builds from Fedora repos**  
      Since June 2016, OVMF is available in the default Fedora repositories as a part of the `edk2-ovmf` package. It would most likely be installed already on a default Fedora installation and the package also includes the firmware for secureboot.  
      ```console
      $ sudo dnf install edk2-ovmf -y
      ```
   2. **Nightly builds from custom repo**  
      The nightly builds of OVMF can be found in a custom repository maintained by Gerd Hoffmann on his personal site where a collection of QEMU/KVM firmware, including EDK2/OVMF can be found. Due to their experimental nature, these builds can be occasionally broken.  
      ```console
      $ sudo dnf install dnf-plugins-core
      $ sudo dnf config-manager --add-repo http://www.kraxel.org/repos/firmware.repo
      $ sudo dnf install edk2.git-ovmf-x64
      ```
2. Navigate to the following directory where the OVMF assets are installed.  
   ```console
   $ cd /usr/share/edk2/ovmf
   $ ls
   EnrollDefaultKeys.efi
   OVMF_CODE.fd
   OVMF_CODE.secboot.fd
   OVMF_VARS.fd
   OVMF_VARS.secboot.fd
   Shell.efi
   UefiShell.iso
   ```
3. Assets from this folder would be continually referred to in the dealings with QEMU.  
