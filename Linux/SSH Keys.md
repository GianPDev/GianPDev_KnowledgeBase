---
tags: [ssh, mosh, sysadmin, bash, connect, connection, remote, security, key, keys, linux, windows]
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
chmod -R 755 ~/.ssh
#or 

chmod -R 700 ~/.ssh
```

#### Revoke ssh key fingerprint:
```bash
ssh-keygen -R server.ip.here
```
with port
```bash
ssh-keygen -R "[server.ip.here]:PORT"
```

### Convert linux ssh key from ssh2 to PEM and back
**WARNING**: This will overwrite the key, but is easily converted back
```bash
ssh-keygen -p -f id_rsa -m PEM
```
```bash
ssh-keygen -p -f id_rsa -m SSH2
```