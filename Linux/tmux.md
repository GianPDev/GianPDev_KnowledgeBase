---
tags: [ssh, mosh, sysadmin, bash, connect, connection, remote, multiplexer, screen, tmux, multiwindow]
---
#### Git install with my settings (Ubuntu)
ubuntu_install_git_tmux.sh
```bash
# Don't forget to make it executable
chmod +x ubuntu_install_git_tmux.sh
```

```sh
#!/bin/bash
sudo apt install -y autotools-dev automake pkg-config libevent-dev libncurses-dev bison byacc
git clone https://github.com/tmux/tmux.git
cd tmux
./autogen.sh
./configure
make
sudo make install

echo "Fix tmux colors"
cat << 'EOF' >> "$HOME/.tmux.conf"
set -ga terminal-overrides ",$TERM:Tc"
# This tmux statusbar config was created by tmuxline.vim
# https://github.com/edkolev/tmuxline.vim
#main bg color #1b1c36
set -g status-justify "left"
set -g status "on"
set -g status-left-style "none"
# Middle section
set -g message-command-style "fg=#1b1c36,bg=#686f9a"
set -g status-right-style "none"
set -g status-style "none,bg=default"
# Active border on pane
set -g pane-active-border-style "fg=#5ccc96"
# When commands are run
set -g message-style "fg=#0f111b,bg=#b3a1e6"
# Inactive border on pane
set -g pane-border-style "fg=#686f9a"
set -g status-right-length "100"
set -g status-left-length "100"
setw -g window-status-activity-style "none"
# Separator colors
setw -g window-status-separator ""
setw -g window-status-style "none,fg=#686f9a,bg=#30365F"
# Left
set -g status-left "#[fg=#0f111b,bg=#30365F] #S #[fg=#30365F,bg=#1b1c36,nobold,nounderscore,noitalics]"
# Right
set -g status-right "#[fg=#1b1c36,bg=default,nobold,nounderscore,noitalics]#[fg=#686f9a,bg=default] %Y-%m-%d  %H:%M #[fg=#30365F,bg=default,nobold,nounderscore,noitalics]#[fg=#1b1c36,bg=#30365F] #h "
# Inactive window
setw -g window-status-format "#[fg=#686f9a,bg=#1b1c36] #I #[fg=#686f9a,bg=#1b1c36] #W "
# Active window
setw -g window-status-current-format "#[fg=#1b1c36,bg=#686f9a,nobold,nounderscore,noitalics]#[fg=#1b1c36,bg=#686f9a] #I #[fg=#1b1c36,bg=#686f9a] #W #[fg=#686f9a,bg=#1b1c36,nobold,nounderscore,noitalics]"
EOF
```


#### Git install with my settings (Centos/RHEL/RockyLinux)
centos_install_git_tmux.sh
```bash
# Don't forget to make it executable
chmod +x centos_install_git_tmux.sh
```

```sh
#!/bin/bash

sudo dnf config-manager --set-enabled powertools

sudo dnf install epel-release

sudo yum install -y protobuf-devel ncurses-devel zlib-devel openssl-devel libevent-devel

git clone https://github.com/tmux/tmux.git

cd tmux

./autogen.sh

./configure

make

sudo make install

echo "Fix tmux colors"

cat << 'EOF' >> "$HOME/.tmux.conf"

set -ga terminal-overrides ",$TERM:Tc"

# This tmux statusbar config was created by tmuxline.vim

# https://github.com/edkolev/tmuxline.vim

#main bg color #1b1c36

set -g status-justify "left"

set -g status "on"

set -g status-left-style "none"

# Middle section

set -g message-command-style "fg=#1b1c36,bg=#686f9a"

set -g status-right-style "none"

set -g status-style "none,bg=default"

# Active border on pane

set -g pane-active-border-style "fg=#5ccc96"

# When commands are run

set -g message-style "fg=#0f111b,bg=#b3a1e6"

# Inactive border on pane

set -g pane-border-style "fg=#686f9a"

set -g status-right-length "100"

set -g status-left-length "100"

setw -g window-status-activity-style "none"

# Separator colors

setw -g window-status-separator ""

setw -g window-status-style "none,fg=#686f9a,bg=#30365F"

# Left

set -g status-left "#[fg=#0f111b,bg=#30365F] #S #[fg=#30365F,bg=#1b1c36,nobold,nounderscore,noitalics]"

# Right

set -g status-right "#[fg=#1b1c36,bg=default,nobold,nounderscore,noitalics]#[fg=#686f9a,bg=default] %Y-%m-%d  %H:%M #[fg=#30365F,bg=default,nobold,nounderscore,noitalics]#[fg=#1b1c36,bg=#30365F] #h "

# Inactive window

setw -g window-status-format "#[fg=#686f9a,bg=#1b1c36] #I #[fg=#686f9a,bg=#1b1c36] #W "

# Active window

setw -g window-status-current-format "#[fg=#1b1c36,bg=#686f9a,nobold,nounderscore,noitalics]#[fg=#1b1c36,bg=#686f9a] #I #[fg=#1b1c36,bg=#686f9a] #W #[fg=#686f9a,bg=#1b1c36,nobold,nounderscore,noitalics]"

EOF
```