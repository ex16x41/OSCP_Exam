# Crunch

ref : [http://adaywithtape.blogspot.com/2011/05/creating-wordlists-with-crunch-v30.html](http://adaywithtape.blogspot.com/2011/05/creating-wordlists-with-crunch-v30.html)

![](../.gitbook/assets/image%20%2828%29.png)

### To know the length of the password list

* crunch 

### Example 1

* `crunch 6 6 ABCD1234 -o outfile1.txt`
  * first `6` : is the minimum length of the string
  * second `6` : is the maximum length of the string
  * `ABCD1234` : charset, are the characters to use during creating string
  * `-o outfile1.txt` : the result will be outputed to a file named "outfile1.txt"

### Crunch Character list

`cat /usr/share/crunch/charset.lst`

### Example 2

* `crunch 4 4 -f /usr/share/crunch/charset.lst mixalpha -o mixedalpha.txt`

### Crunch Character Translation

* `@` , lower case alpha characters
* `,` , upper case alpha characters
* `%` , numeric characters
* `^` , special characters\(including spaces\)

### Example 3

pattern : Abc\#$012

* `crunch 8 8 -t ,@@^^%%% | more`



