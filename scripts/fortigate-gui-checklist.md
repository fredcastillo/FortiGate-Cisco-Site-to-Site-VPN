# FortiGate-B — GUI checklist used in Infrastructure 2

## Network

- port1: `203.0.113.26/30`
- port2: `10.21.75.129/28`

## VPN

Path: `VPN > IPsec Tunnels > VPN-TO-SITE-A`

### Phase 1

- Remote Gateway: `203.0.113.21`
- IKEv2
- DES-SHA256
- DH14
- Pre-shared key configured on both peers

### Phase 2

- Local: `10.21.75.128/28`
- Remote: `10.21.75.0/25`
- DES-SHA256
- PFS enabled
- DH14

## Routing

- Default route via `203.0.113.25` / port1
- Route to `10.21.75.0/25` via `VPN-TO-SITE-A`, using the gateway value retained from the lab implementation

## Policies

- LAN/Server → VPN: NAT disabled
- VPN → LAN/Server: NAT disabled
- `WEBSERVER_A_INTERNET`: port2 → port1, NAT enabled

## Functional proof

1. IPsec Monitor = UP
2. Browser-PC reaches `10.21.75.130`
3. Traceroute reaches the server
4. Disable `VPN-TO-SITE-A` administratively from Network → Interfaces
5. Communication fails
6. Re-enable the interface
7. Communication returns
