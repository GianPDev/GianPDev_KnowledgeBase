---
tags: [ssh, mosh, sysadmin, bash, connect, connection, remote, security]
---
- [[SSH Certificate Based Authentication (CA Signing Keys)]]

#### Generate Key Pair (Recommended Settings)
```bash
ssh-keygen -t rsa -b 4096
```

##### Copy Public key to Remote host
```bash
# on main computer ssh-copy-id to remote computer
ssh-copy-id USER@server.ip.here
# enter password
```

#### Copying Public Key to Remote Host (windows 10, powershell)
```powershell
Get-Content -Path "$env:USERPROFILE/.ssh/id_rsa.pub" | ssh USER@server.ip.here "cat >> .ssh/authorized_keys"
```

#### Give correct permissions to .ssh files:
```bash
chmod 755 ~/.ssh
chmod 755 ~/.ssh/authorized_keys
```

#### Revoke ssh key fingerprint:
```bash
ssh-keygen -R server.ip.here
```