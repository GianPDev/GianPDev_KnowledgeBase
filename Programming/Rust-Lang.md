---
tags: [rust, programming, dev]
---
[[Zola Static Site Generator]]
[[Miniserve website server]]
[[Dioxus]]

### Creating Projects
#### Create Project with Folder
Choose --bin or --lib
```bash
cargo new --bin/lib project-name
```
#### Creating Project within Folder
Choose --bin or --lib
```bash
cargo init --bin/lib
```

### Good Clippy Settings
Based from here: https://youtu.be/ifaLk5v3W90?t=645
```rust
#![warn(
    clippy::pedantic,
    clippy::nursery,
    clippy::unwrap_used,
    clippy::expect_used,
    clippy::perf
)]
```
Run in CI or before committing, will auto fix code: if possible
```bash
cargo clippy --fix -- -W clippy::pedantic -W clippy::nursery -W clippy::unwrap_used -W clippy::expect_used
```

### Check code via clippy in realtime
```bash
cargo install --locked bacon
```
```bash
bacon clippy
```

### Manually installing rust-analyzer on linux (last known working version for stable)
```bash
mkdir -p ~/.local/bin && curl -L https://github.com/rust-lang/rust-analyzer/releases/download/2022-08-15/rust-analyzer-x86_64-unknown-linux-gnu.gz | gunzip -c - > ~/.local/bin/rust-analyzer && chmod +x ~/.local/bin/rust-analyzer
```
```bash
#in neovim
:CocConfig
```
```bash
vi ~/.config/nvim/coc-settings.json
```
add:
```json
"rust-analyzer.server.path": "~/.local/bin/rust-analyzer"
```
should look like this
```json
{                                
  "eslint.autoFixOnSave": true,                                
  "eslint.filetypes": ["javascript", "javascriptreact", "typescript", "typescriptreact"],                               
  "coc.preferences.formatOnSaveFiletypes": ["*"],
  "tsserver.formatOnType": true,                                               
  "coc.preferences.formatOnType": true,                         
  "suggest.noselect": true,                                            
  "coc.preferences.extensionUpdateCheck": "daily",           
  "rust-analyzer.server.path": "~/.local/bin/rust-analyzer"                       
} 
```

### Other Rust Analyzer Fix:
```bash
rustup toolchain install nightly --component rust-analyzer-preview
```
```bash
#in neovim
:CocConfig
```
```bash
vi ~/.config/nvim/coc-settings.json
```
add:
```json
"rust-analyzer.server.path": "~/.rustup/toolchains/nightly-x86_64-unknown-linux-gnu/bin/rust-analyzer"
```

The cause of the issue is that the latest stable release is using glibc 2.8 or higher, which is incompatible with OS's like ubuntu 18.04, RHEL/RHEL based 8.
Other programs might be affected by this, as ubuntu 18.04 is being deprecated by github actions and assumedly other programs.
Related issue threads:
https://github.com/rust-lang/rust-analyzer/issues/13081
https://github.com/rust-lang/rust-analyzer/issues/11558