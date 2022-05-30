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