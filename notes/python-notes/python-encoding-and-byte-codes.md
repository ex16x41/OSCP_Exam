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

* Sequence of characters :   `éspanol`
* Sequence of bytes : 
* In Python 2, `str` is a sequence of bytes and `unicode` is a sequence of characters.
*  In Python 3, this is changed; `bytes` is a sequence of bytes and `str` is a sequence of characters. And by default all string are in "UTF-8", hence _"str is sequence of character"_ makes sense.
* There are 3 kinds of literals
  * String and Byte literal : `r'Simple'` and `b'Simple'`
  * String literal concat : `"hello" 'world'` == `"helloworld"`
  * Formatted string literals : `f'{n:03o}'`

![Formatted string literals](../../.gitbook/assets/image%20%28142%29.png)

![https://docs.python.org/3/reference/lexical\_analysis.html](../../.gitbook/assets/image%20%28140%29.png)

[https://docs.python.org/3/reference/lexical\_analysis.html](https://docs.python.org/3/reference/lexical_analysis.html)

{% embed url="https://late.am/post/2012/03/26/exploring-python-code-objects.html" %}

[Imp : https://stackoverflow.com/questions/62648171/encode-string-as-octal-utf-8-python-3](https://stackoverflow.com/questions/62648171/encode-string-as-octal-utf-8-python-3)

## Generate byte code

* We can only generate byte code using the below functions. But we cannot automate both bytecode generation and execution, becuase python string append some unwanted characters due to which 

```text
# Python3
class OctUTF8:
  def __init__(self,s):
      self.s = s.encode()
  def __repr__(self):
      return "b'" + ''.join(f'\\{n:03o}' for n in self.s) + "'"
 
 
 
 # Python2
 def byte_code_octal(source):
	encoded = ""
	for character in source:
		character = character.encode('utf8')
		character = '%(#)03o' % {"#": ord(character)}
		encoded = encoded + "\\" + character
	return encoded
```

![](../../.gitbook/assets/image%20%28145%29.png)

## Generate byte code python2

d



