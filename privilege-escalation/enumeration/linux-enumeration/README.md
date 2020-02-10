# Linux Enumeration

* route
* history
* searching for files with SUID privileges.
* [https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/](https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/)

### 1\) To check if a service is installed or not

* whereis nc
* rpm -qa
* dpkg -l
* File locations
  *  **/usr/src/**
  *  **/usr/local/src**
  *  **/opt/**
  *  **/var/**
* \*\*\*\*

![whereis](../../../.gitbook/assets/image%20%2861%29.png)



Basic Enumerations • Find worldwritable folders and files. \(Eg. In DDL injection, we need to write file to a given location. So if a library folder or file is worldwritables then we could modify existing DLL \) find / -xdev -type d -perm -0002 -ls 2&gt; /dev/null find / -xdev -type f -perm -0002 -ls 2&gt; /dev/null

```text
• Find root files with worldwritable permissions or non administrator like authenticated users.


• Find SUIDs and SGIDs (linux specific check)
    ○ find / -perm -4000 -user root -exec ls -ld {} \; 2> /dev/null
    ○ find / -perm -2000 -group root -exec ls -ld {} \; 2> /dev/null
• OS and services versions
    ○ cat /etc/*-release
    cat /etc/issue

    ○ cat /proc/version
    uname -a
    dmesg | grep Linux 

• Environment variables and terminal enumeration
    cat /etc/profile
    cat /etc/bashrc
    cat ~/.bash_profile
    cat ~/.bashrc
    cat ~/.bash_logout
    printenv
    set

    cat ~/.bash_history
    history


• What applications are installed. (Like searching if python, perl, ruby, c++ is installed or not)
    ls -al /usr/bin/ or /bin/ or /sbin/

    dpkg -l
    rpm -qa

• Interesting and configuration files
    cat /etc/syslog.conf
    cat /etc/chttp.conf
    cat /etc/lighttpd.conf
    cat /etc/cups/cupsd.conf
    cat /etc/inetd.conf
    cat /etc/apache2/apache2.conf
    cat /etc/my.conf
    cat /etc/httpd/conf/httpd.conf
    cat /opt/lampp/etc/httpd.conf
    www-data@alpha:/var/www/html$ find . -iname '*config*'

• Scheduled tasks
    crontab -l
    ls -alh /var/spool/cron
    ls -al /etc/ | grep cron
    ls -al /etc/cron*
    cat /etc/cron*
    cat /etc/at.allow
    cat /etc/at.deny
    cat /etc/cron.allow
    cat /etc/cron.deny
    cat /etc/crontab
    cat /etc/anacrontab
    cat /var/spool/cron/crontabs/root


• Search for plain text passwords
    grep -i user [filename]
    grep -i pass [filename]
    grep -C 5 "password" [filename]
    www-data@alpha:/var/www/html$ grep -R '$bigtree\["config"\]\["db"\]' .
    find . -name "*.php" -print0 | xargs -0 grep -i -n "var $password"   # Joomla

• Session management
    lsof -t -i:4444
```

```text
Operating System
	• What's the distribution type? What version?
	• What's the kernel version? Is it 64-bit?
	• What can be learnt from the environmental variables?
	• Is there a printer?


Applications & Services
	• What services are running? Which service has which user privilege?
	• Which service(s) are been running by root? Of these services, which are vulnerable - it's worth a double check!
	• What applications are installed? What version are they? Are they currently running?
	• Any of the service(s) settings misconfigured? Are any (vulnerable) plugins attached?
	• What jobs are scheduled?
	• Any plain text usernames and/or passwords?


Communications & Networking
	• What NIC(s) does the system have? Is it connected to another network?
	• What are the network configuration settings? What can you find out about this network? DHCP server? DNS server? Gateway?
	• What other users & hosts are communicating with the system?
	• Whats cached? IP and/or MAC addresses
	• Is packet sniffing possible? What can be seen? Listen to live traffic
	
	
Is port forwarding possible? Redirect and interact with traffic from another view
	Note: FPipe.exe -l [local port] -r [remote port] -s [local port] [local IP]
	Note: ssh -[L/R] [local port]:[remote ip]:[remote port] [local user]@[local ip]
	Note: mknod backpipe p ; nc -l -p [remote port] < backpipe | nc [local IP] [local port] >backpipe
	
Is tunnelling possible? Send commands locally, remotely
	ssh -D 127.0.0.1:9050 -N [username]@[ip]
	proxychains ifconfig

Confidential Information & Users
	• Who are you? Who is logged in? Who has been logged in? Who else is there? Who can do what?
	• What sensitive files can be found?
	• Anything "interesting" in the home directorie(s)? If it's possible to access
	• Are there any passwords in; scripts, databases, configuration files or log files? Default paths and locations for passwords
	• What has the user being doing? Is there any password in plain text? What have they been edting?
	• What user information can be found?
	• Can private-key information be found?
	
	
File Systems
	• Which configuration files can be written in /etc/? Able to reconfigure a service?
	• What can be found in /var/ ?
	• Any settings/files (hidden) on website? Any settings file with database information?
	• Is there anything in the log file(s) (Could help with "Local File Includes"!)
	• If commands are limited, you break out of the "jail" shell?
	• How are file-systems mounted?
	• Are there any unmounted file-systems?
	• What "Advanced Linux File Permissions" are used? Sticky bits, SUID & GUID
	• Where can written to and executed from? A few 'common' places: /tmp, /var/tmp, /dev/shm
	• Any "problem" files? Word-writeable, "nobody" files


Preparation & Finding Exploit Code
	• What development tools/languages are installed/supported?
How can files be uploaded?
```

