
#### Install fish (ubuntu)
```bash
sudo apt install fish
```

#### Install Fisher Plugin Manager (Run in fish shell)
```bash
curl -sL https://raw.githubusercontent.com/jorgebucaran/fisher/main/functions/fisher.fish | source && fisher install jorgebucaran/fisher
```

#### Get nvm (node version manager) working with fish
With nvm installed using bash and fisher installed in fish, run in fish shell:
```bash
fisher install FabioAntunes/fish-nvm edc/bass
```
