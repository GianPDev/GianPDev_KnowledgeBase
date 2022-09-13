---
tags: [git, ssh, gpg, keys, commit, config, repo, download, github]
---

### Undo last commit (without discarding new files)
```bash
git reset --soft HEAD~1
```
#### Setting up Git for commits
```bash
git config --global user.email "EMAILNAME@EMAILPLACE.com"
git config --global user.name "John S. Smith"
```

#### Storing Login Details in RAM cache
*Doesn't seem to be working for me atm, need to do more research*
```bash
git config --global credential.credentialStore cache
```

This stores the credentials in a plaintext file in `~/.git-credentials`
```bash
git config --global credential.helper store
```

### Signing git commits and getting verified commits on github
[[GPG-Keys#Generate Primary GPG Key]]

### Download latest released binary of a repo
Getting latest deb file and sha of neovim: 
```bash
URL=$(wget https://api.github.com/repos/neovim/neovim/releases/latest -O - | awk -F \" -v RS="," '/browser_download_url/ {print $(NF-1)}'| sed '/.deb/!d'); wget $URL
```

Gets latest and last binary file in Assets (recommend using sed to filter the extension like above)
```bash
URL=$(wget https://api.github.com/repos/<USER>/<REPO>/releases/latest -O - | awk -F \" -v RS="," '/browser_download_url/ {print $(NF-1)}'); wget $URL -O $(basename "$URL")
```

### Git clone one specific folder
Copied from: https://stackoverflow.com/a/69801161/11951047
```bash
git clone --no-checkout https://github.com/git/git
cd git
git sparse-checkout init --cone
# that sets git config core.sparseCheckoutCone true
git sparse-checkout set folder1/folder2
git read-tree -mu HEAD
```

### Git move changed uncommitted work to a new branch
```bash
git checkout -b <new-branch>
```