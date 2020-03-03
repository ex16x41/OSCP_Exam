# New Security Features

Ref: [https://www.digitalocean.com/community/tutorials/how-to-use-port-knocking-to-hide-your-ssh-daemon-from-attackers-on-ubuntu](https://www.digitalocean.com/community/tutorials/how-to-use-port-knocking-to-hide-your-ssh-daemon-from-attackers-on-ubuntu)

## 1. Port Knock

* what to do about services that you want access to, but do not want to expose to everybody.
* Port knocking is one method of obscuring the services that you have running on your machine.
* It allows your firewall to protect your services until you ask for a port to be opened through a specific sequence of network traffic.
* Even more helpful is that there is **no feedback given on knocking attempts**.

### 1.1 How does port knockd works

* Port knocking works by configuring a service to watch firewall logs or packet capture interfaces for connection attempts.
* If a specific sequence of predefined connection attempts \(or “knocks”\) are made, the service will modify the firewall rules to open up connections on a certain port.
* In this way, port knocking adds an additional layer that a user must go through to even get to the regular authentication.
* * 
