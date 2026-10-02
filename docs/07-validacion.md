# 07 — Validación

## VPN activa

El Cisco mostró una IKEv2 SA en estado `READY` y `show crypto ipsec sa` mostró encapsulación, cifrado, decapsulación y descifrado de paquetes.

## Comunicación

El usuario alcanzó `10.21.75.130` y accedió al servicio HTTPS.

## Traceroute

```text
1  10.21.75.1
2  * * *
3  10.21.75.130
```

## VPN deshabilitada

Se deshabilitó administrativamente la interfaz lógica `VPN-TO-SITE-A` en la GUI del FortiGate. La comunicación hacia `10.21.75.130` dejó de funcionar.

## VPN restaurada

Al volver a habilitar la interfaz VPN, la comunicación con el Web Server se restableció.

![VPN UP](../images/07-connectivity-vpn-up.png)

![VPN DOWN](../images/09-vpn-disabled-failure.png)

![VPN RESTORED](../images/10-vpn-restored.png)
