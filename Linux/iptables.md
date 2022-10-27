---
tags: [firewall, iptables, rules, security, linux, sysadmin, portforward, portforwarding, ssh]
---
##### Show ip rules
```bash
sudo iptables -L --line-numbers
# shows port numbers instead of text
sudo iptables -L --line-numbers -n
```

#### Delete Rule
```bash
# delete rule
sudo iptables -D INPUT 6
```

#### Add Rule
```bash
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

#### Delete ALL rules (VERY UNSAFE, BACKUP FIRST)
```bash
# F for flush I assume
iptables -F
```

### Restore iptables config (after saving using `iptables-save`)
```bash
sudo iptables-restore < /etc/iptables.rules
```

### Permanently enable iptables rrules
```bash
sudo yum install iptables-services -y
# restore/change iptables (make sure it works and can ssh)
```
```bash
sudo systemctl start iptables
sudo systemctl enable iptables
sudo systemctl status iptables
```
```bash
sudo systemctl disable firewalld.service
sudo systemctl stop firewalld.service
```
Login to root then:
```bash
iptables-save >/etc/sysconfig/iptables
```