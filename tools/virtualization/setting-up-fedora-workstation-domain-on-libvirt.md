---
title: Setting up Fedora Workstation domain on libvirt  
subsection: virtualization  
order: 8  
---

# Setting up Fedora Workstation domain on libvirt

1. Download the Fedora Workstation ISO file from website and store it in a reference directory `cdromimg`.  
   ```
   https://getfedora.org
   ```
2. Create a virtual disk image of type `16GB` and of format `RAW` in a reference directory `datadrct` by executing the following command.  
   ```console
   $ qemu-img create -f raw datadrct/fedovirt.raw 16G
   ```
3. Invoke virt-install session for installing Fedora Workstation using BIOS on the virtual disk image by executing the following command on the host.  
   ```console
   $ virt-install \
       --virt-type kvm \
       --name fedoraXX-mstr \
       --memory 4096 \
       --vcpus 8 \
       --cdrom cdromimg/Fedora-Workstation-Live-x86_64-xx-y.z.iso \
       --disk datadrct/fedoraXX/fedoraXX-mstr.raw \
       --graphics vnc,listen=0.0.0.0,port=5920 \
       --network default,mac=00:00:00:00:03:00 \
       --noautoconsole \
   ```
   OR  
   Invoke virt-install session for installing Fedora Workstation using UEFI on the virtual disk image by executing the following command on the host.  
   ```console
   $ virt-install \
       --virt-type kvm \
       --name fedoraXX-mstr \
       --memory 4096 \
       --vcpus 8 \
       --cdrom cdromimg/Fedora-Workstation-Live-x86_64-xx-y.z.iso \
       --disk datadrct/fedoraXX/fedoraXX-mstr.raw \
       --graphics vnc,listen=0.0.0.0,port=5920 \
       --network default,mac=00:00:00:00:03:00 \
       --noautoconsole \
       --boot uefi
   ```
   The following is an example output for the above command.  
   ```
   Starting install...
   
   Domain is still running. Installation may be in progress.
   You can reconnect to the console to complete the installation process.
   ```
4. Execute the following command on the host to list currently defined domains. The `--all` flag lists all domains - even if they are running or not.  
   ```console
   $ virsh list --all
    Id   Name            State
   -------------------------------
    1    fedoraXX-mstr   running
   ```
5. Visit https://www.realvnc.com/en/connect/download/viewer/ in an internet browser of choice, download and install the VNC viewer application either on the host device or another device in the same network.  
6. Switch to the VNC Viewer window and type in `0.0.0.0:5920` from the host device (or `<ip-address-of-host-device>:5920` if accessed from another device in the same network) to continue installing.  
7. A greeting window would open up inside the VNC Viewer, providing with two options - Either to `Try Fedora` or `Install to Hard Drive`.  
   ![01](/content/tools/virtualization/images/setting-up-fedora-workstation-domain-on-libvirt/01.png)  
8. Now, follow either the instructions [**Setting up Fedora Workstation VM on QEMU using BIOS**](/tools/virtualization/setting-up-fedora-workstation-vm-on-qemu-using-bios.html) guide if BIOS is being used or [**Setting up Fedora Workstation VM on QEMU using UEFI**](/tools/virtualization/setting-up-fedora-workstation-vm-on-qemu-using-uefi.html) guide if UEFI is being used to complete the installation.  
9. Once the installation is completed, power off the domain. It would show up like the following when listed on the host.  
   ```console
   $ virsh list --all
    Id   Name            State
   -------------------------------
    1    fedoraXX-mstr   shut off
   ```
10. It can be started up again by executing the following command on the host.  
    ```console
    $ virsh start fedoraXX-mstr
    Domain 'fedoraXX-mstr' started
    ```
    Switch to the VNC Viewer window and type in `0.0.0.0:5920` from the host device (or `<ip-address-of-host-device>:5920` if accessed from another device in the same network) to continue using the domain.  
11. To power off a domain externally, simply execute the following command from the host.  
    ```console
    $ virsh shutdown fedoraXX-mstr
    Domain 'fedoraXX-mstr' is being shutdown
    ```
12. If the domain has become unresponsive to the shutdown command, it can be forcibly turned off by executing the following command from the host.  
    ```console
    $ virsh destroy fedoraXX-mstr
    Domain 'fedora34-mstr' destroyed
    ```
13. If the domain is no longer required, it can be unlisted by executing the following command from the host.  
    ```console
    $ virsh undefine fedoraXX-mstr
    Domain 'fedora34-mstr' has been undefined
    ```
    Note that this would not remove the virtual disk image, the installation sources and other related elements for the domain and they must be removed manually.  
14. To edit the configuration of the domain, execute the following command from the host.  
    ```console
    $ virsh edit fedoraXX-mstr
    ```
    This would open up the domain's XML configuration specification in the default text editor of the host. Follow https://libvirt.org/formatdomain.html to learn more about it.  
