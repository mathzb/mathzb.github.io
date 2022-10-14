# Simpel VLAN routing

```shell title="Opret VLAN med navn og ID"
/interface vlan add name=VLAN2 vlan-id=2 interface=Lan disabled=no
```

```shell title="Tildel IP adresser til VLAN interfaces"
/ip address add address=192.168.10.1/24 interface=VLAN2
```

!!! note

    Tildeling af DHCP Server kan laves via WinBox ved hjælp af DHCP Wizarden
