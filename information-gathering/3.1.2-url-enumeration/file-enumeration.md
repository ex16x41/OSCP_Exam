# File Enumeration

## Chosing the righ extensions

### HTB Boxes

* Windows
  * **EXT** = Understand the underlying technology used, and chose your extensions based on this
  * 1
    * **EXT**, __html, txt
  * 2

## Dirsearch

* dirsearch.py -u [http://10.10.10.10](http://10.10.10.10) -e asp,aspx,bat,c,cfm,cgi,com,dll,exe,htm,html,inc,jhtml,jsa,jsp,log,mdb,nsf,php,phtml,pl,reg,sh,shtml,sql,txt,xml,/,js -x 403,400 –json-report=\[/path/\]dirsearch.json

## Gobuster

* gobuster -u http://192.168.2.62/dvwa -w /usr/share/dirbuster/wordlists/directory-list-lowercase-2.3-small.txt -t 40 -x .php, .txt, .html

