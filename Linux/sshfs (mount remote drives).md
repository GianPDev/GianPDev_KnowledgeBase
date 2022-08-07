### Mount remote drive (tested on termux>Fedora36 with root)
Make directory to mount drive:
```bash
mkdir -p ~/mnt/FOLDERNAME
```
Mount remote drive:
```bash
sshfs USER@SERVER:/home/USER/ ~/mnt/FOLDERNAME -o reconnect
```
`-o reconnect` reconnects drive when disconnected
unmount remote drive:
```bash
fusermount -u ~/mnt/FOLDERNAME
```