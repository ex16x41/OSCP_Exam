---
description: >-
  When normal nmap scan is not able to help, then we need to use a kind of
  advance/custom scan to fulfill our needs.
---

# 8.2 NSE scripts

Link : [https://nmap.org/book/nse-usage.html](https://nmap.org/book/nse-usage.html)

## Types of NSE scripts

* **Prerule scripts**
  * These run before host discovery. These scripts are run when nmap has not collected any information about its targets yet.
  * Example : dns-zone-transfer
* **Host scripts**
  * These run after {host discovery, port scanning, version detection, and OS detection}.
  * There are rules which govern which host script to be applied on which host.
  * Example : whois-ip, path-mtu
* **Service scripts**
  * While port scanning we get a list of open ports. These open ports run some services on them. So based on which service is running, that particular service script is applied.
  * Example : There are 15 http service scripts that is run when port 80 \(http\) is open.
* **Postrule scripts**
  * These scripts run after Nmap has scanned all of its targets. 
  * They can be useful for formatting and presenting Nmap output.
  * These scripts could print a reverse-index of the Nmap output—showing which hosts run a particular service.

## Introduction to NSE Scripts

Nmap NSE scripts are written in [LUA](http://www.lua.org/) programming language. Script scanning is normally done in combination with a port scan, because scripts may be run or not run depending on the port states found by the scan.

* `-Pn` option
  * it is to run a script scan without a host discovery i.e. treat all hosts as online, **only port scan**.  
  * This technique is useful for scripts like `whois-ip` that only use the remote system's address and don't require it to be up.
* `-sn` option 
  * it is to run a script scan without a port scan, **only host discovery** like a simple ping. 
* `-sS` option 
  * it is is for TCP SYN \(Stealth\) Scan. SYN scan is relatively unobtrusive and stealthy, since it never completes TCP connections.  It also allows clear, reliable differentiation between `open`, `closed`, and `filtered` states.

## Using Nmap NSE scripts

* Nmap NSE scripts are stored in "/usr/share/nmap/scripts/"
* We could get details of the NSE script using:
  * nmap --script-help=http-wordpress-users.nse
  * These details does not give details on the arguments, but there is link present in these details which points for details on arguments.

![](../../../.gitbook/assets/image%20%2859%29.png)

### Example 1

`nmap  --script http-default-accounts --script-args "http-default-accounts.basepath='/admin', category='web', fingerprintfile=/usr/share/nmap/nselib/data/http-default-accounts-fingerprints.lua"`

