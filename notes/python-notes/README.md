# Python notes

## Processing JSON data

```text
import json

# Note that json is very picky of using of " or '
# the overall must always be '
# Error : "{'session': '12345'}"
# Correct : '{"session": "12345"}'


data = [{"id":1,"name":"2","position":"3","email":"a","src":"5"}]
r = json.loads(data)
print(data[0]["id"]
```

## exec\(\) function

![](../../.gitbook/assets/image%20%28137%29.png)

## python string and literals

![](../../.gitbook/assets/image%20%28140%29.png)

{% embed url="https://late.am/post/2012/03/26/exploring-python-code-objects.html" %}

[Imp : https://stackoverflow.com/questions/62648171/encode-string-as-octal-utf-8-python-3](https://stackoverflow.com/questions/62648171/encode-string-as-octal-utf-8-python-3)

