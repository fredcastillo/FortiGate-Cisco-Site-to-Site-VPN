# 04 — FortiGate-B

## Interfaces

| Interfaz | Dirección |
|---|---:|
| port1 | `203.0.113.26/30` |
| port2 | `10.21.75.129/28` |
| VPN-TO-SITE-A | interfaz lógica del túnel |

## VPN — GUI

Ruta:

`VPN > IPsec Tunnels > VPN-TO-SITE-A`

### Phase 1

- Remote Gateway: `203.0.113.21`
- IKEv2
- DES-SHA256
- DH14
- PSK

### Phase 2

- Local: `10.21.75.128/28`
- Remote: `10.21.75.0/25`
- DES-SHA256
- PFS habilitado
- DH14

## Policies

- `LAN → VPN`: port2 → VPN-TO-SITE-A, NAT off.
- `VPN → LAN`: VPN-TO-SITE-A → port2, NAT off.
- `WEBSERVER_A_INTERNET`: port2 → port1, NAT on.

## Evidencia

![VPN](../images/02-vpn-fortigate-b.png)

![Policies](../images/03-policies-fortigate-b.png)
