# Python byte code

## Generate byte code

* We can only generate byte code using the below functions. But we cannot automate both bytecode generation and execution, because python string append some unwanted characters due to which 

{% tabs %}
{% tab title="Python3" %}
```text
# Python3

class OctUTF8:
  def __init__(self,s):
      self.s = s.encode()
  def __repr__(self):
      return "b'" + ''.join(f'\\{n:03o}' for n in self.s) + "'"
```
{% endtab %}

{% tab title="Python2" %}
```text
 # Python2
 
 def byte_code_octal(source):
	encoded = ""
	for character in source:
		character = character.encode('utf8')
		character = '%(#)03o' % {"#": ord(character)}
		encoded = encoded + "\\" + character
	return encoded
```
{% endtab %}
{% endtabs %}



![](../../../.gitbook/assets/image%20%28145%29.png)



## Executing byte code directly \(manually\)

* You can always copy byte code directly in order to execute as shown below in python3.
* For this we will only use `print("yes!! code executed")` as our command.

![python3](../../../.gitbook/assets/image%20%28150%29.png)

![python2](../../../.gitbook/assets/image%20%28153%29.png)

* Now here I have manually converted `print("yes!! code executed")` to bytecode `\160\162\151\156\164\050\042\171\145\163\041\041\042\051`

## Note possible : Executing byte code \(automation\)

* If you want to automate this directly, you will get error.

{% tabs %}
{% tab title="Python3" %}
```text
# Python3

class ByteCode_octal:
  def __init__(self,s):
      self.s = s.encode()
  def __repr__(self):
      return ''.join(f'\\{n:03o}' for n in self.s)
      
cmd = 'print("yes!!")'
enc = str(ByteCode_octal(cmd))		# to convert from obj to str
print('Encoded cmd to byte code : {}'.format(enc))
print('')
print('')
exec(enc)
```

![](../../../.gitbook/assets/image%20%28152%29.png)
{% endtab %}

{% tab title="Python2" %}
```text
def ByteCode_octal(source):
	encoded = ""
	for character in source:
		character = character.encode('utf8')
		character = '%(#)03o' % {"#": ord(character)}
		encoded = encoded + "\\x" + character
	return encoded

cmd = 'print("yes!!")'
enc = ByteCode_octal(cmd)
print('Encoded cmd to byte code : %s' % enc)
print('')
print('')
exec(enc)
```

![Error when tried to exec\(\) byte code](../../../.gitbook/assets/image%20%28147%29.png)
{% endtab %}
{% endtabs %}

* The problem is that python string when defined add some bytes at the end of the string that are not accessible to edit, as these are required for python strings to work. We cannot print these unwanted bytes or remove these bytes.
* So this ends here.

## Alternatively, we could generate byte code for only special characters

* We could evade sandbox and character filtering by encoding, characters filtered using byte code.
* Below is python2 example.

### Byte encoding special characters

* If I tried to replace characters using re.sub\(\) I get error when code is executed.

{% tabs %}
{% tab title="Python3" %}
```text
# Python3

cmd = 'print("yes!!")'
cmd = re.sub('\(', '\\\\x28', cmd)
# cmd = re.sub('\(', r'\\x28', cmd)
# cmd = cmd.replace('(','\\x28')

print(cmd)
print('')
print('')
exec(cmd)
```

![](../../../.gitbook/assets/image%20%28148%29.png)
{% endtab %}

{% tab title="Python2" %}
```text
# Python2

cmd = 'print("yes!!")'
cmd = re.sub('\(', '\\\\x28', cmd)
# cmd = re.sub('\(', '\\x28', cmd)
# cmd = re.sub('\(', r'\\x28', cmd)
# cmd = cmd.replace('(','\\x28')

print(cmd)
print('')
print('')
exec(cmd)
```

![python2](../../../.gitbook/assets/image%20%28149%29.png)
{% endtab %}
{% endtabs %}

* But if do anything you cannot execute python byte code automatically, you need to manually set the string.



{% tabs %}
{% tab title="Python3" %}
```text
# Python3

cmd = 'print("yes!!")'
cmd = cmd.replace('(', '\\x28')

print(cmd)
print('')
print('')
exec(cmd)
```

![](../../../.gitbook/assets/image%20%28148%29.png)
{% endtab %}

{% tab title="Python2" %}
```text
# Python2

cmd = 'print("yes!!")'
cmd = re.sub('\(', '\\\\x28', cmd)
# cmd = re.sub('\(', '\\x28', cmd)
# cmd = re.sub('\(', r'\\x28', cmd)

print(cmd)
print('')
print('')
exec(cmd)
```

![python2](../../../.gitbook/assets/image%20%28149%29.png)
{% endtab %}
{% endtabs %}



* B



