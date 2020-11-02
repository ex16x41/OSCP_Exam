---
description: Includes python formatting
---

# Python byte code and encodings

## Python formatting

### Simple formatting

```text
# Python3
txt = "For only {} dollars!"
price=49
print(txt.format(price))

# Python2
price=49
print('For only {} dollars!' % price)
```

* We intended simply to put value in the position, hence the .format\(\) will accept variable or value only

### Precision formatting

```text
# Python3
txt = "For only {pos:.2f} dollars!"
price = 49
print(txt.format(pos = price))

# Python2
input1 = "Python"
input2 = 2
print '%(language)s has %(#)03d quote types.' % {'language': input1, "#": input2}
```

* In string "txt" if we want to precision then we need to use the above formatting.
* The .format\(\) **accepts only key value pairs**, it does not accept integer value or a variable

![Error example because .format\(\) accepts key:value pairs](../../.gitbook/assets/image%20%28139%29.png)



## Python Literals

* There are 3 kinds of literals
  * String and Byte literal : `r'Simple'` and `b'Simple'`
  * String literal concat : `"hello" 'world'` == `"helloworld"`
  * Formatted string literals : `f'{n:03o}'`

![Formatted string literals](../../.gitbook/assets/image%20%28142%29.png)

![https://docs.python.org/3/reference/lexical\_analysis.html](../../.gitbook/assets/image%20%28140%29.png)

[https://docs.python.org/3/reference/lexical\_analysis.html](https://docs.python.org/3/reference/lexical_analysis.html)

{% embed url="https://late.am/post/2012/03/26/exploring-python-code-objects.html" %}

[Imp : https://stackoverflow.com/questions/62648171/encode-string-as-octal-utf-8-python-3](https://stackoverflow.com/questions/62648171/encode-string-as-octal-utf-8-python-3)

## Generate byte code python3

```text
class OctUTF8:
  def __init__(self,s):
      self.s = s.encode()
  def __repr__(self):
      return "b'" + ''.join(f'\\{n:03o}' for n in self.s) + "'"
```

![](../../.gitbook/assets/image%20%28143%29.png)

## Generate byte code python2

d



