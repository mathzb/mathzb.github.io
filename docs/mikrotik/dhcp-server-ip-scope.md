# Basic DHCP & IP Scope commands

```shell title="Deaktiver DHCP Server"
/ip dhcp-server disable "Lan DHCP Server"
```

```shell title="Aktiver DHCP Server"
/ip dhcp-server enable "Lan DHCP Server"
```

```shell title="Skift DNS"
/ip dhcp-server network set 0 dns-server=8.8.8.8,8.8.4.4
```

```shell title="Ændre Scope & DHCP"
/ip pool set Lan ranges=10.10.0.10-10.10.0.254
/ip dhcp-server network set 0 address=10.10.0.0/24 gateway=10.10.0.1 netmask=24
/ip address set 0 address=10.10.0.1/24 interface=bridge-local network=10.10.0.0
```

```shell title="DHCP Reservation"
/ip dhcp-server lease add address=10.10.0.XX mac-address=00:04:13:77:XX:XX server="Lan DHCP Server" comment="NAVN"
```

```shell title="Se DHCP Lease"
/ip dhcp-server lease print
```

```shell title="Slet DHCP Lease"
/ip dhcp-server lease remove "ID"
```
