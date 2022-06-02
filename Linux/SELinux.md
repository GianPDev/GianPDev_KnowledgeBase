---
tags: [firewall, firewalld, iptables, security, linux, sysadmin, portforward, portforwarding]
---
#### Check if SELinux is enabled
```bash
sestatus
getenforce
```

#### Set SELinux to permissive
```bash
setenforce 0
```