---
tags: [security, linux, ssh, sshd, config, password, passwordless, ssh, sshkeys]
---
[[SSH Keys]]
[[Firewalls]]
[[SELinux]]

### Backup sshd_config and ssh_config (RHEL systems seem to use sshd_config)
```bash
cp /etc/ssh/ssh_config /etc/ssh/ssh_config~
```
```bash
cp /etc/ssh/sshd_config /etc/ssh/sshd_config~
```

### Disabling passwords (prevents brute force attacks)
**IMPORTANT:** Make sure [[SSH Keys]] are working otherwise root will be **impossible** to access without reinstall of OS
In `/etc/ssh/sshd_config`:
```bash
PasswordAuthentication no
```
Restart sshd to apply changes:
```bash
systemctl restart sshd
```