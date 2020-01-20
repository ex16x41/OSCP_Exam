# Python notes

### New socket connection

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

