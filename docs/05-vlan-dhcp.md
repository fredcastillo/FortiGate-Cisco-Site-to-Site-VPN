# 05 — VLAN 10 y DHCP

## Switch-A

El running-config recibido confirma:

```text
GigabitEthernet0/0 → access VLAN 10
GigabitEthernet0/1 → access VLAN 10
GigabitEthernet0/2 → access VLAN 10
```

## DHCP

El Cisco 7200 entrega DHCP para `10.21.75.0/25` con gateway `10.21.75.1` y rango efectivo `.10–.100`.

![VLAN y DHCP](../images/04-vlan-dhcp.png)
