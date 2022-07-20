---
tags: [bash, linux, server, shell, fish, visudo]
---
[[bash utilities]]
[[fish shell]]

#### Change default shell to fish
```bash
chsh -s /usr/bin/fish
```
It will then prompt you to enter your password

#### Change default shell back to bash
```bash
chsh -s /bin/bash
```

#### Change default visudo editor
```bash
sudo update-alternatives --config editor
```

#### set ownership of folder to current user
```bash
chown -R $(whoami) ~/FOLDER
```