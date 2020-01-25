# Windows Enumeration

### Enumerate user and user privileges

* cmd prompt
  * net users
  * net user _username_ 
  * whoami /all

### Enumerate OS version

* cmd prompt
  * systeminfo

### print file contents

* type file1.txt

### print file path

* file file1.txt

### Search for files and folders with Admin privileges writable by other users

![](../../.gitbook/assets/image%20%2851%29.png)

## Changing permissions of a file

![](../../.gitbook/assets/image%20%2830%29.png)

![](../../.gitbook/assets/image%20%2845%29.png)

![](../../.gitbook/assets/image%20%2857%29.png)

{% embed url="https://www.cyberciti.biz/tips/windows-change-access-permissions-from-the-command-line.html" %}

* C : change \(Modify\)

## List Services in windows

*  tasklist /SVC

## Print environment variables

* set

## Accesschk

to know what kind of accesses specific users or groups have to resources including files, directories, Registry keys, global objects and Windows services.

## Creating a new user with admin rights

{% embed url="https://operating-systems.wonderhowto.com/how-to/create-admin-user-account-using-cmd-prompt-windows-0125689/" caption="reference" %}

```text
net user /add [*username] [password]
net localgroup administrators [username] /add
```

