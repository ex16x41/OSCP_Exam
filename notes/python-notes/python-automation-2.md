# Python Automation 1

## Sessions request

```text
import requests
import re

def TestRequest(filename):
    
    url = "http://10.10.10.93/transfer.aspx"
    
    s = requests.session()
    
    # For GET requests
    r = s.get(url)
    print(r.text)
    
    # For post requests
    
    
TestRequest("Please Subscribe")
```

## Example 1 : Serialized POST request automation for upload bypass

![request](../../.gitbook/assets/image%20%28120%29.png)

![python automation](../../.gitbook/assets/image%20%28121%29.png)

Here burp was used to validate if the request is generate properly.

![final script](../../.gitbook/assets/image%20%28122%29.png)

