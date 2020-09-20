# Need of NOPs in BO

[Ref](https://l3nsec.blog/2018/03/25/brainpan-1-oscp-vulnhub-walkthrough/) : 

If we do not give nops in our buffer overflow payload. The following behavior happens.

```text
#payload without nops

JMP_ESP = 0x311712f3

shellcode = ""
shellcode += "\xbd\x67\x82\x22\x2a\xdd\xc2\xd9\x74\x24\xf4\x58"
...

payload = 'A' * 524
payload += struct.pack("I", JMP_ESP) # encode the int
payload += shellcode
payload += '\r\n'
```

![ida\_brainpan\_crash\_ill.png](https://l3nblog.files.wordpress.com/2018/03/ida_brainpan_crash_ill.png?w=663)

Aaaaaand it crashed.

I got pretty confused, I had never used msf payloads for exploitation and I even read other walkthroughs on this machine but all used a nop slide which to be fair didn’t make sense to me since we knew exactly what was the ESP address.

Until I proceeded to single step in the shellcode and notice this instruction:

![ida\_brainpan\_shellcode.png](https://l3nblog.files.wordpress.com/2018/03/ida_brainpan_shellcode.png?w=663)

So… ESP points to 0x0028F920, and that instruction is, according to [Intel’s manual](https://software.intel.com/en-us/articles/intel-sdm#combined), this is storing the _FPU operating environment_ to _\[esp-0xC\]_, so this is overwriting our instructions!

We can check this by single-stepping the instruction:

![x32dbg\_brainpan\_instructions\_overwritten.png](https://l3nblog.files.wordpress.com/2018/03/x32dbg_brainpan_instructions_overwritten.png?w=663)

This is why we need to use a nop slide.

