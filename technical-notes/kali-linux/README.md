# Kali linux

### ftp

* `ftp 192.168.1.1`
* `binary` : changing the mode of transfer from ASCII to binary. Used for transferring windows executable.

### File system hierarchy

{% embed url="http://www.pathname.com/fhs/pub/fhs-2.3.html" %}

### Lack of TTY support

* A shell is command line interpreter.
* A terminal is a text input/output environment.
* A console is a physical terminal
* "TeleTYpe" \(aka TTY\) - can be found in "/dev/tty\*". They are devices that acts like a "teletype" \(such as a terminal\).
* "Pseudo-TeletYpe" \(aka PTY\) - These are devices that acts like a terminal to the process reading/writing there, but managed by something else. **So we can use PTY to fake TTY**.

## File Permission

![1000](../../.gitbook/assets/image%20%2850%29.png)

### Check mount permissions

* `mount`

![](../../.gitbook/assets/image%20%2842%29.png)

### Creating a NFS mount

cherry notes

