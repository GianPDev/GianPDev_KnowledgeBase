
## Common Commands
> The following examples will use the following:
> IPv4: 192.168.1.0/24 
> aka 
> IPv4: 192.168.1.0 Subnet: 255.255.255.0
> Usable Host IPv4 Range:	192.168.1.1 - 192.168.1.254
> Broadcast: 192.168.1.255
> 
> IPv6 0:0:0:0:0:::0/64
> Full IP Address:	0000:0000:0000:0000:0000:0000:0000:0000
> Total IP Addresses:	18,446,744,073,709,551,616
> Network:	0000:0000:0000:0000::
> IP Range:	0000:0000:0000:0000:0000:0000:0000:0000 - 0000:0000:0000:0000:ffff:ffff:ffff:ffff
> 
> Device Name: eth0

Check route to see how networking is connecting
```bash
ip route get 1.1.1.1
```
Show all network interfaces (ethernet/wifi)
```bash
ip a
```
Show running interfaces
```bash
ip link ls up
```
Flush (delete) the IP address from the interface
```bash
ip -s -s a f to 192.168.1.0/24
```
Set device to up (turn on)
```bash
ip link set dev eth0 up
```
Set device to down (turn off)
```bash
ip link set dev eth0 down
```
assign ip to device/interface
```bash
ip a add 192.168.1.2/24 dev eth0
```
add route to ip
```bash
ip route add 192.168.1.2/24 via 192.168.1.0
```