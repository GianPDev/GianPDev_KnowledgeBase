
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