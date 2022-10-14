# Oprettelse af nyt netværk

```shell title="Opret Pool Range"
/ip pool set Lan ranges=172.16.20.10-172.16.20.254
```

```shell title="Sæt addresse og netværk"
/ip address set [find where interface=Lan] address=172.16.20.1/24 comment="default configuration" interface=Lan network=172.16.20.0
```

```shell title="Opret DHCP netværk på LAN interface"
/ip dhcp-server network set [find where interface=Lan] address=172.16.20.0/24 comment="Lan DHCP" dns-server=8.8.8.8,8.8.4.4 gateway=172.16.20.1 netmask=24
```

```shell title="Aktiver DHCP Server samt navngiv"
/ip dhcp-server set "Lan DHCP Server" disabled=no
```

```shell title="Giv Mikrotik en statistk DNS server"
/ip dns static set 0 address=1.1.1.1 name=router
```
