### Default ports
`3000 for website`
`3001 for hot-reload`
*quick line to ssh tunnel (need to forward both ports for hot-reload)*
```bash
ssh -v -L 3000:127.0.0.1:3000 -f -N user@server
```
