# 01 — Arquitectura

## Propósito

Interconectar mediante IPsec una red de usuarios ubicada detrás de un Cisco 7200 con una red de servidor ubicada detrás de un FortiGate.

## Componentes

- Cisco 7200: gateway, DHCP, NAT e IPsec del Sitio A.
- FortiGate-B: firewall, NAT e IPsec del Sitio B.
- Router-ISP: tránsito WAN.
- Switch-A: VLAN 10.
- PC1 / Browser-PC: pruebas.
- Web Server: Debian + Apache + HTTPS.

## Arquitectura

![Topología](../images/01-topology-gns3.png)

## Flujo

```text
Usuarios → Cisco 7200 → IPsec → FortiGate-B → Web Server
```

## Objetivo de validación

La comunicación debe existir con el enlace VPN habilitado, desaparecer cuando la interfaz VPN se deshabilita administrativamente y regresar cuando se habilita de nuevo.
