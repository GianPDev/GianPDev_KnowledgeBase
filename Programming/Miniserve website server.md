---
tags: [rust, webdev, server, web, website, miniserve, html, spa]
---
#### Serve Website with port
```bash
# cargo install miniserve
miniserve . -p 1111
```

#### Serve SPA Website
```bash
# cargo install miniserve
miniserve . -p 1111 --spa --index index.html
```