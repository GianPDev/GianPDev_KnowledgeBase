
#### Install Mosh (Centos/RHEL/RockyLinux)
install_git_mosh.sh
```bash
# make executable
chmod +x install_git_mosh.sh
```

*This works with [[SELinux]] set to permissive*


```sh
#!/bin/bash

sudo dnf config-manager --set-enabled powertools

sudo dnf install epel-release

sudo yum install -y protobuf-devel ncurses-devel zlib-devel openssl-devel

git clone https://github.com/mobile-shell/mosh.git

cd mosh

./autogen.sh

./configure

make

sudo make install

# iptables

sudo iptables -A INPUT -p udp --dport 60000:61000 -j ACCEPT

# firewalld port forward

sudo firewall-cmd --zone=public --add-port=60000-61000/udp --permanent
```