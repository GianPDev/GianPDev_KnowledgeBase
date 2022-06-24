---
tags: [ssh, mosh, sysadmin, bash, connect, connection, remote, development, dev, tunnel]
---
#### SSH Tunnel
By ssh tunnelling, you can work on a website on a remote server and test it like it's on your local network! 
*In this case you can connect to http://localhost:1111/ on your server which is hosted on port 1112*
```bash
#ssh -L LOCAL_PORT:LocalHost:REMOTE_PORT -N -f -l username remote_server_ip
```

```bash
ssh -L 1111:127.0.0.1:1112 -N -f -l username remote_server_ip
```