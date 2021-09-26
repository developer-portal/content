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
   ![01](https://user-images.githubusercontent.com/49605954/127772125-23b95312-87ce-4e82-aeb5-401b250e6eed.png)  
4. In a new terminal session on the guest, execute the following command to the enable the `OpenSSH` service.  
   ```console
   $ sudo systemctl enable --now sshd.service
   ```
   ![02](https://user-images.githubusercontent.com/49605954/127771828-59a3a95f-1340-45ed-bea3-73030018c453.png)  
5. Now change the password of the current user by executing the following command in the terminal session on the guest.  
   ```console
   $ passwd
   ```
   ![03](https://user-images.githubusercontent.com/49605954/127772003-96037412-7ed4-4ffb-bb0c-ca86444a5dc3.png)  
6. In a new terminal session on the host, execute the following command to connect to the guest using `SSH`.  
   ```console
   $ ssh liveuser@localhost -p 2323
   ```
   ![04](https://user-images.githubusercontent.com/49605954/127772578-737aa4c2-ef6d-45da-8443-10bf6829b561.png)  
   OR  
   In a new terminal session on a device connected to the same network, execute the following command to connect to the guest using `SSH`.  
   ```console
   $ ssh liveuser@<ip-address-of-the-host-device> -p 2323
   ```
   ![05](https://user-images.githubusercontent.com/49605954/127772551-81c53fa0-b53c-40d9-a0c0-6516368692d9.png)  
7. Execute the following command in to logout of the session.  
   ```console
   $ logout
   ```
8. This was an example of mapping port 22 of the virtualized guest with port 2323 of the host with TCP for the purposes of SSH and this can be reused with slight changes to accommodate other use-cases.  
