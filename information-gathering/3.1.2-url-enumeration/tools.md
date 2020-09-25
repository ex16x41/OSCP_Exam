# Directory Enumeration

## Gobuster

* gobuster dir -w /usr/share/dirbuster/wordlists/directory-list-lowercase-2.3-medium.txt -s 200,204,301,302,307,400,401,403,405,500 -t 20 --url 10.10.10.82
  * -t 20 number of threads
  * -s allowed status code
  * dir specifies the scan is either directory scanning or file scanning. Hence it is compulsory for both file and dir enumeration.

## Wfuzz

* d

