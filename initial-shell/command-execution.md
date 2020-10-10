# Command Execution

## 1. Using log files

### Example 1 : PHP + LFI

* If we have a php page that prints the file contents as below.

```text
# This page is vulnerable to LFI attacks on http parameter "file"
<?php

echo include($_REQUEST["file"])

?>
```

* What this does it includes a file inside a php context _\(this is the main reason why its vulnerable\)_
* As the PHP webpage is vulnerable to LFI, we could prints contents of that given we have permissions to read it. \(generally, **www-data** user\)
* Now objective is to find interseting files which could print user defined inputs. Example
  * **/etc/logs/auth.log**
    * needs ssh to be accessible, login with username, where username is used to supply user inputs
  * **/etc/logs/apache2/access.log**
    * edit user-agent header field of get requests to supply user inputs
* Using /etc/logs/auth.log method,
  * For exploiting auth.log we need to have SSH port accessible, which will be enabled generally.
  * Then we try to log in with user `<?php system("whoami"); ?>` 
  * `ssh '<?php system("whoami"); ?>'@10.10.10.81`
  * This login attempt will create a log entry in auth.log file

![successful command execution](../.gitbook/assets/image%20%28126%29.png)



