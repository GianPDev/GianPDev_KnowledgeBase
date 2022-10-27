
### Important for network debugging
run this
```bash
systemctl restart networking
```
then tests like
```bash
ping 1.1.1.1
```

For different domain providers (my case is porkbun, don't forget to enable API access on domain manager), look here: https://github.com/acmesh-official/acme.sh/wiki/dnsapi2 (also check web GUI's: ACME>Challenge Plugins> Add>DNS API drop down menu for your DNS)
Securing Proxmox ([Source](https://loicpefferkorn.net/2020/11/secure-proxmox-ve-management-interface-with-two-factor-authentication-reverse-proxy-and-lets-encrypt-certificate/))
![[Securing Proxmox.pdf]]

*Note: I had the "This site can't be reached"*