---
tags: [bash, linux, server, ip, port, tcp, udp, used]
---
### Find used port and what's using it, and kill it
```bash
lsof -i tcp:8080
```
```bash
# sample output
COMMAND       PID     USER   FD   TYPE   DEVICE SIZE/OFF NODE NAME
rootlessp 1234567 USERNAME    4u  IPv6 DEVICENO      0t0  TCP localhost:irdmi->localhost:49280 (ESTABLISHED)
```
```bash
kill -9 1234567
```
