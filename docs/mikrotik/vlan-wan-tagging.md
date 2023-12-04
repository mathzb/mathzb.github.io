# Vlan WAN Tag

I nogen tilfælde så bliver man nødtil at VLAN tagge sit WAN interface for at kunne få tildelt en IP Adresse fra sin ISP. \\
Hvis dette ikke gøres, så får man ikke internetadgang. \\

Log på WINBOX og derefter tryk på **"Interfaces"** -> Opret et VLAN ved at trykke på "+" ikonet i toppen af venstre hjørne i det nye vindue.

| Type | Beskrivelse |
| -------------- | ---|
| `Name`     | F.eks. VLAN-WAN |
| `VLAN ID`     | Oplyst fra ISP |
| `Interface` | ether1 (Internet) |

Resten skal forblive default.  

Derefter gå til **Interface List** → Og tryk på **WAN**, og ændre **Interface** til dit nylig oprettet VLAN.  

Den sidste ting der skal gøres nu er at opdatere DHCP Client til at forespørge på det rigtige VLAN Interface.  
I menuen til venstre tryk på **"IP" → "DHCP Client"** og dobbeltklik på **defcon**.

| Type | Beskrivelse |
| -------------- | ---|
| `Interface`     | Dit nylig oprettet VLAN |
| `Use Peer DNS`     | false |
| `Use Peer NTP` | false |
| `Add Default Route` | Yes |

Resten skal være default.
