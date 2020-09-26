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



