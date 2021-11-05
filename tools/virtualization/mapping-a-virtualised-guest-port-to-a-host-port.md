---
title: Mapping a virtualized guest port to a host port  
subsection: virtualization  
order: 10  
---

# Mapping a virtualized guest port to a host port

1. Download the Fedora Workstation ISO file from website and store it in a reference directory `cdromimg`.  
   ```
   https://getfedora.org
   ```
2. Start a virtual machine for mapping a virtualized guest port to a host port for the live ISO and there is no need for a virtual disk image here.  
   ```console
   $ qemu-system-x86_64 \
       -boot menu=on \
       -m 4096 \
       -cpu max \
       -smp 4 \
       -cdrom cdromimg/<Fedora-Workstation-Live-x86_64-xx-y.z.iso> \
       -accel kvm \
       -net nic \
       -net user,hostfwd=tcp::2323-:22
   ```
3. Wait for the virtual machine to boot up.  
   ![01](/content/tools/virtualization/images/mapping-a-virtualised-guest-port-to-a-host-port/01.png)  
4. In a new terminal session on the guest, execute the following command to the enable the `OpenSSH` service.  
   ```console
   $ sudo systemctl enable --now sshd.service
   ```
   ![02](/content/tools/virtualization/images/mapping-a-virtualised-guest-port-to-a-host-port/02.png)  
5. Now change the password of the current user by executing the following command in the terminal session on the guest.  
   ```console
   $ passwd
   ```
   ![03](/content/tools/virtualization/images/mapping-a-virtualised-guest-port-to-a-host-port/03.png)  
6. In a new terminal session on the host, execute the following command to connect to the guest using `SSH`.  
   ```console
   $ ssh liveuser@localhost -p 2323
   ```
   ![04](/content/tools/virtualization/images/mapping-a-virtualised-guest-port-to-a-host-port/04.png)  
   OR  
   In a new terminal session on a device connected to the same network, execute the following command to connect to the guest using `SSH`.  
   ```console
   $ ssh liveuser@<ip-address-of-the-host-device> -p 2323
   ```
   ![05](/content/tools/virtualization/images/mapping-a-virtualised-guest-port-to-a-host-port/05.png)  
7. Execute the following command in to logout of the session.  
   ```console
   $ logout
   ```
8. This was an example of mapping port 22 of the virtualized guest with port 2323 of the host with TCP for the purposes of SSH and this can be reused with slight changes to accommodate other use-cases.  
