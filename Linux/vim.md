---
tags: [ssh, mosh, sysadmin, bash, editing, editor, texteditor, dev, developer, vi, vim, neovim, nano]
---

### Save as sudo when editing system file as non-sudo
```vim
:w !sudo tee %
```
*Can press `L` to load and see changes (read only)*

#### Special in shell command mode
```bash
vim -E
```

#### Launch Vim with no settings
```bash
vim -u NONE filename.txt
```

### Force filetype for change syntax highlighting
I have a CSS plugin which shows the colors inline, changing files to it activates it
```bash
:setfiletype css
```

#### My Neovim init.vim
replace_init_vim.sh
```bash
curl -OL https://raw.githubusercontent.com/GianPDev/public_files/main/scripts/replace_init_vim.sh
# check the script first! Never run scripts from the internet without checking it!
chmod +x replace_init_vim.sh
./replace_init_vim.sh
```

### Show dos line endings (prevents scripts from running on linux)
```bash
:e ++ff=unix
```

### Delete dos line endings
```bash
:%s/\r$
```
`CTRL+V`, `CTRL+M` to create `^M`
```bash
:%s/^M//g
```