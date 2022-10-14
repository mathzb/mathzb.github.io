# Portforwarding

## Eksemple på portforwarding

| Type           | Beskrivelse                                                                                                                                               |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `dst-port`     | Porten der skal komme trafik ind på (188.180.38.24:4353)                                                                                                  |
| `protocol`     | Protokollen trafikken kommer ind på (tcp eller udp)                                                                                                       |
| `to-addresses` | Den interne IP adresse trafikken skal dirigeres til (192.168.100.100)                                                                                     |
| `to-ports`     | Den port i det interne netværk trafikken skal dirigeres til. Hvis denne ikke bliver udfyldt kommer trafikken på samme port som pakkerne er kommet ind på. |
| `in-interface` | Denne SKAL være sat. Hvis ikke bliver alt trafik ramt af port forward reglen og dirigeret til to-addresses.                                               |

```shell
/ip firewall nat add action=dst-nat chain=dstnat dst-port=xxxx in-interface=Internet protocol=xxx to-addresses=xxx.xxx.xxx.xxx to-ports=xxxx
```

---

## DMZ

For at oprette en dmz skal man lave en portforward uden porten

```shell
/ip firewall nat add action=dst-nat chain=dstnat in-interface=Internet to-addresses=xxx.xxx.xxx.xxx
```

!!! warning

    Man skal dog være opmærksom på at hvis man har oprettet en DMZ kan man ikke få fat i routeren udefra!

---
