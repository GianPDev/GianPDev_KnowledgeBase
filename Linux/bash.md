---
tags: [bash, linux, server, shell, fish, visudo, internet, issues]
---
[[bash utilities]]
[[fish shell]]

### Change default shell to fish
```bash
chsh -s /usr/bin/fish
```
It will then prompt you to enter your password

### Change default shell back to bash
```bash
chsh -s /bin/bash
```

### Change default visudo editor
```bash
sudo update-alternatives --config editor
```

### set ownership of folder to current user
```bash
chown -R $(whoami) ~/FOLDER
```

### for loop (foreach doesn't work in almalinux?)
All these assume that there is a txt file called `serverips.txt` with IPs separated by new lines (`enter`, `\n` etc)
```bash
for ip in $(cat serverips.txt); do ssh-copy-id root@$ip; done
```
```bash
for ip in $(cat serverips.txt); do ssh root@$ip passwd USER; done
```
A way to see if all servers are connected (after copying ssh keys)
```bash
for ip in $(cat serverips.txt); do ssh root@$ip "hostnamectl"; echo ""; done
```

Make user sudo without password (has issues with passwords that have special characters)
```bash
for ip in $(cat serverips.txt); do ssh USER@$ip 'hostnamectl; echo ""; sudo echo "USER ALL=(ALL) NOPASSWD:ALL" | sudo -S tee -a /etc/sudoers.d/ansible_admin'; done
```

### Change machine-id
In cases where you clone a machine, they would have the same machine-id
Check your machine-id
```bash
cat /etc/machine-id
```
```bash
# remove or move
/etc/machine-id
```
```bash
sudo systemd-machine-id-setup
```
```bash
cat /etc/machine-id
```