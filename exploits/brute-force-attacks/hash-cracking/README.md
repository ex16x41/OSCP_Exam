# Hash Cracking

*  Instead of brute forcing with list of clear text passwords.
* we could first find hash of the clear text list of passwords.
* Then we compare this hashed list of password during authentication.
* This is an efficient approach is some cases.

## .kdbx keepass database

* To get hash
  * keepass2john 
* To crack hash
  * `hashcat -m 13400 hash.txt /usr/share/seclists/rockyou.txt` \(use this if you know the hashcat module\)
  * `john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt`

