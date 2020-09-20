---
description: Server Message Block Protocol - SMB protocol
---

# 3.1.5 SMB Enumeration

## SMB features

* SMB is used to share file and peripherals along the network.
* complex implementation, have faced many security bugs and vulnerabilities in the past.
* 
There are two approaches to run SMB service.

1. Running SMB service on top of NetBIOS
   * The SMB service runs on port 139/tcp.
2. Running SMB on top of TCP/IP
   * The SMB service runs on port 445/tcp.

## SMB Versions

* SMB1 – Windows 2000, XP and Windows 2003. 
* SMB2 – Windows Vista SP1 and Windows 2008 
* SMB2.1 – Windows 7 and Windows 2008 R2 
* SMB3 – Windows 8 and Windows 2012.

## Pre-requisiste of SMB enumeration

1\) Check if SMB services are running in windows hosts.

![](../../../.gitbook/assets/image-33.png)

2\) The file and sharing service should be enabled on all network so that we could access the shared  files.

![](../../../.gitbook/assets/image-16.png)

3\) If you have not given the proper permissions for sharing you will get the below error.

![](../../../.gitbook/assets/image-40.png)

## SMB Enumeration

![](../../../.gitbook/assets/image-74.png)

