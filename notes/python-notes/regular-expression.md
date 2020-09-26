# Python RE

## Reference :

{% embed url="https://docs.python.org/2/library/re.html" %}



* `val = re.findall(r'PHPSESSION="(.*?)"', requestfile)[0]` 
  * This will find all occurrences, such that it will fetch only the value part starting with `PHPSESSION="` and then `(.*?)` all the data will be fetched until `"` is hit. The output will not contain double quotes.
  * It will search from `requestfile`.
  * `[0]` means print only the first occurrence of the find.

