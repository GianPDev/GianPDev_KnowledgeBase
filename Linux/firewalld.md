---
tags: [firewall, firewalld, security, linux, sysadmin, portforward, portforwarding, ssh]
---

#### Show Firewall Rules
```bash
sudo firewall-cmd --list-all
```
#### Add service to port forward
```bash
sudo firewall-cmd --permanent --zone=public --add-service=http

sudo firewall-cmd --permanent --zone=public --add-service=https

```
#### Refresh firewall
```bash
sudo firewall-cmd --reload
```
