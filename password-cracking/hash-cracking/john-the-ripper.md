# John the ripper

Given we have hash dump stored in `hashes.txt`

![](../../.gitbook/assets/image%20%2843%29.png)

* John the ripper has pattern matching feature which could identify generic hashes only. Automatically.

## Using john.conf custom rules

* during password proofing we get a list of string to work with.
* We could add/mutate the list to a more password oriented list like including numbers in every string at the last.
* To do this, we could use john.conf to do it efficiently.
* We just need to and an extra rule.

![](../../.gitbook/assets/image%20%2810%29.png)

![](../../.gitbook/assets/image%20%282%29.png)

* `john --wordlist=file1.txt --rules --stdout > mutated.txt`
  * `--rules` : specifies john the ripper to use rules.

ref : [https://www.gracefulsecurity.com/custom-rules-for-john-the-ripper/](https://www.gracefulsecurity.com/custom-rules-for-john-the-ripper/)

