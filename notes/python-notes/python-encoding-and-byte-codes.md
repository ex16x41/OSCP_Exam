---
description: Includes python formatting
---

# Python byte code and encodings

## Python formatting

### Simple formatting

```text
txt = "For only {} dollars!"
price=49
print(txt.format(price))
```

* We intended simply to put value in the position, hence the .format\(\) will accept variable or value only

### Precision formatting

```text
txt = "For only {price:.2f} dollars!"
print(txt.format(price = 49))
```

* In string "txt" if we want to precision then we need to use the above formatting.
* The .format\(\) **accepts only key value pairs**, it does not accept integer value or a variable

![](../../.gitbook/assets/image%20%28139%29.png)



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

d

## Generate byte code python2

d



