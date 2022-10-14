# Statisk IP på WAN

`Print` kan med fordel bruges undervejs hvis du ikke er sikker på interface navn mm.

```shell title="Sæt IP på WAN interface"
/ip address add address=xxx.xxx.xxx.xxx/SUBNETPREFIX interface=Internet
```

```shell title="Sæt default gateway"
/ip route add distance=1 gateway=xxx.xxx.xxx.xxx
```

```shell title="Deaktiver DHCP på WAN"
/ip dhcp-client remove numbers=0
```

```shell title="Sæt DNS"
/ip dns set servers=xxx.xxx.xxx.xxx,xxx.xxx.xxx.xxx
```
