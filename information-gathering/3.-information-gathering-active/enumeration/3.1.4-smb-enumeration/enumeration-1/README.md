# 3.1.5.1 SMB NetBIOS Enumeration

Ref: [https://www.hackingarticles.in/netbios-and-smb-penetration-testing-on-windows/](https://www.hackingarticles.in/netbios-and-smb-penetration-testing-on-windows/)

NBT : netbios over tcp

The SMB NetBIOS34 service listens on TCP ports 139 and 445, as well as several UDP ports.

Tools such as nmap, nbtscan, etc. could be used for enumeration of NetBIOS services.

![](../../../../../.gitbook/assets/image-53.png)

![](../../../../../.gitbook/assets/image-4.png)



### NetBIOS provides three distinct services:

1. Name service \(NetBIOS-NS\) for name registration and resolution via port **137**.
2. Datagram distribution service \(NetBIOS-DGM\) for connection less communication via port **138**.
3. Session service \(NetBIOS-SSN\) for connection-oriented communication via port **139**. ****

