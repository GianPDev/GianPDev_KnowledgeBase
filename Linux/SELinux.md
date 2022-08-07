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

### Actually managing SELinux
https://teamignition.us/selinux-practical-intro-to-audit2why-and-audit2allow.html
https://computingforgeeks.com/manage-selinux-status-context-ports-booleans-using-ansible/

Useful Ansible collections:
[[Ansible#Useful Ansible Collections]]