---
description: Includes python formatting
---

# Python byte code and encodings

## Python formatting

### Simple formatting

{% tabs %}
{% tab title="Python3" %}
```text
# Python3

txt = "For only {} dollars!"
price=49
print(txt.format(price))
```
{% endtab %}

{% tab title="Python2" %}
```text
# Python2

price=49
print('For only {} dollars!' % price)
```
{% endtab %}
{% endtabs %}

* We intended simply to put value in the position, hence the .format\(\) will accept variable or value only

### Precision formatting

{% tabs %}
{% tab title="Python3" %}
```text
# Python3

txt = "For only {pos:.2f} dollars!"
price = 49
print(txt.format(pos = price))
```
{% endtab %}

{% tab title="Python2" %}
```text
# Python2

input1 = "Python"
input2 = 2
print '%(language)s has %(#)03d quote types.' % {'language': input1, "#": input2}
```
{% endtab %}
{% endtabs %}

* In string "txt" if we want to precision then we need to use the above formatting.
* The .format\(\) **accepts only key value pairs**, it does not accept integer value or a variable

![Error example because .format\(\) accepts key:value pairs](../../../.gitbook/assets/image%20%28139%29.png)



## Python Literals

### Introduction

* Sequence of characters :   `éspanol`
* Sequence of bytes \(in octal form\) : `\160\162\151\156\164\050\042\171\145\163\041\041\042\051`
* Sequence of bytes \(in hex form\) : `\x70\x72\x69\x6e\x74\x28\x22\x79\x65\x73\x21\x21\x22\x29`
* In Python 2, `str` is a sequence of bytes and `unicode` is a sequence of characters. Python2 accepts only ASCII string.
*  In Python 3, this is changed; `bytes` is a sequence of bytes and `str` is a sequence of characters. And by default all string are in "UTF-8", hence _"str is sequence of character"_ makes sense.

### Python3 literals 

* There are 3 kinds of literals
  * String and Byte literal : `r'Simple'` and `b'Simple'`
  * String literal concat : `"hello" 'world'` == `"helloworld"`
  * Formatted string literals : `f'{n:03o}'`

![Formatted string literals](../../../.gitbook/assets/image%20%28142%29.png)

![https://docs.python.org/3/reference/lexical\_analysis.html](../../../.gitbook/assets/image%20%28140%29.png)

[https://docs.python.org/3/reference/lexical\_analysis.html](https://docs.python.org/3/reference/lexical_analysis.html)

{% embed url="https://late.am/post/2012/03/26/exploring-python-code-objects.html" %}

[Imp : https://stackoverflow.com/questions/62648171/encode-string-as-octal-utf-8-python-3](https://stackoverflow.com/questions/62648171/encode-string-as-octal-utf-8-python-3)



