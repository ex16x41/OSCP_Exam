# File Permission

## UID vs eUID ?

Ref : [https://www.osso.nl/blog/setuid-seteuid-uid-euid/](https://www.osso.nl/blog/setuid-seteuid-uid-euid/)

They're different when a program is running set-uid. Effective UID is the user you changed to, UID is the original user.

```text
id -u    # is the EUID
id -u -r # is the UID
```

## File Permission

* Ref :
*  [https://www.samba.org/samba/docs/old/Samba3-HOWTO/AccessControls.html](https://www.samba.org/samba/docs/old/Samba3-HOWTO/AccessControls.html)
* [https://serversitters.com/how-to-calculate-linux-permissions.html](https://serversitters.com/how-to-calculate-linux-permissions.html)



![ref : http://ptgmedia.pearsoncmg.com/images/chap4\_9780321613226/elementLinks/04-09-xsan-posix.jpg](../../.gitbook/assets/image%20%2860%29.png)

![http://permissions-calculator.org/](../../.gitbook/assets/image%20%2822%29.png)

![1000](../../.gitbook/assets/image%20%2846%29.png)

![2000](../../.gitbook/assets/image%20%2871%29.png)

* 3000 is when set : "setgid" & "sticky bit"
* 4000 is when set : "setuid"
* 7000 is when set : "setgid" & "sticky bit" & "setuid"

![](../../.gitbook/assets/image%20%2863%29.png)

![](../../.gitbook/assets/image%20%2845%29.png)

## What does it means when a user is in root group

* Requirements to exploit this:
  * We generally aim to run a malicious script as root user.
  * If a non-root user is in root group, and we have a file whose owner is root and is in root group. We need "group execute" permission must be set on the file. If this requirement is set then we could execute the file.
  * But we aim to execute custom malicious script, to do this we need "write" permissions on that file.
  * But even if we do not have permissions to write the file, if the group execute permission is set for all linux commands, then we just need to find a linux command which could execute shell code.
  * If we found such a command, then we could execute "/bin/bash" or "/bin/sh" using this command to get root shell. 

