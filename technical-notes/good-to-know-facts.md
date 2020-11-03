# Good To know facts

## 1. ASCII vs Utf-8

* ASCII was designed as 7-bit encoding, where as UTF-8 is 8-bit encoding.
  * ASCII ranges from \(0 , 127\)
  * UTF-8 ranges from  \(0 , 256\)
  * Although 8 bit is used and we call it as ASCII-compatible characters
* Utf-8 could represent the complete unicode characters.
* ASCII is a subset of UTF-8 encoding.
  * They are both are byte encoding
  * ASCII printable characters are a pretty small list \(bytes with values between 32 and 127\)
* I find no good reason to use UTF-8 untill, you want to print characters outside of ASCII. Below is chart for all ASCII character.
* We use UTF-8 when we want to print character in other languages, like chinese or spanish character.

![common ASCII characters](../.gitbook/assets/image%20%28143%29.png)

![Complete ASCII table](../.gitbook/assets/image%20%28144%29.png)

