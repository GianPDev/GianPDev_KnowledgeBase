
#### Generate Primary GPG Key
Follow the Prompts (make sure to backup revoke certificate)
```bash
gpg --full-generate-key
```
#### List Private Keys
```bash
gpg -K
```
#### List Public Keys
```bash
gpg -k
```
### Generate Revoke Certificate Manually
```bash
gpg --output mykey-revoke.asc --gen-revoke mykey
```
### Get Key Signatures (last # of key id)
```bash
gpg --list-signatures
```

#### Importing and getting GPG Private keys to work with git signing
Import private key
```bash
gpg import private-key
```
Can test if it works (most likely won't) by using this:
```bash
echo "test" | gpg --clearsig
```
Get listed keys and note the ID of the imported key (should say \[unknown\])
```bash
gpg -K
```
Edit the key and trust it (enter `5`, then `y`)
```bash
gpg --edit-key <KEYID> trust quit
```
Ensure the `~/.gnupg` is owned by user and chmod -ed correctly
```bash
chown -R $(whoami) ~/.gnupg/
```
```bash
chmod 600 ~/.gnupg/*
```
```bash
chmod 700 ~/.gnupg
```

Restart gpg-agent
```bash
systemctl --user stop gpg-agent
```
```bash
systemctl --user start gpg-agent
```
or
```bash
systemctl --user restart gpg-agent
```
add to .bashrc, then source .bashrc
```bash
export GPG_TTY=$(tty)
```

### Sign Git Commits with GPG Key
```bash
git config --global commit.gpgsign true
git config --global tag.gpgSign true
```
Get signature
```bash
gpg --list-signatures
```
```bash
git config --global user.signingkey {your-key-signature}
```
```bash
git config --global user.email email@emailplace.com
```
```bash
git config --global user.name John Smith
```