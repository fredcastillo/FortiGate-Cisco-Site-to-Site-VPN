# 02 — Direccionamiento

## WAN

| Equipo | Interfaz | IP |
|---|---|---:|
| Cisco 7200 | Gi1/0 | 203.0.113.21/30 |
| Router-ISP | Gi1/0 | 203.0.113.22/30 |
| Router-ISP | Gi2/0 | 203.0.113.25/30 |
| FortiGate-B | port1 | 203.0.113.26/30 |

## LAN Usuarios

- Red: `10.21.75.0/25`
- Gateway: `10.21.75.1`
- VLAN: `10`
- DHCP: `.10–.100`

## LAN Servidor

- Red: `10.21.75.128/28`
- Gateway: `10.21.75.129`
- Web Server: `10.21.75.130`
