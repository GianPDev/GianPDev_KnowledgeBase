---
tags: [rust, programming, dev]
---
[[Zola Static Site Generator]]
[[Miniserve website server]]

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