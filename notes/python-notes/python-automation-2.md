# Python Automation 2

## Sessions request

```text
import requests
import re

def TestRequest(filename):
    url = "http://10.10.10.93/transfer.aspx"
    s = requests.session()
    
    r = s.get(url)
    
    print(r.text)
    
TestRequest("Please Subscribe")
```

## Example 1 : Serialized POST request automation

![request](../../.gitbook/assets/image%20%28119%29.png)

![Python Automation](../../.gitbook/assets/image%20%28118%29.png)

