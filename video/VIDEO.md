# 🎥 Guion de video — VPN Site-to-Site Cisco 7200 y FortiGate

## Enlace final

**YouTube / OneDrive:** `PEGAR-ENLACE-AQUI`

## Duración objetivo

Aproximadamente **6–8 minutos**. El límite de la asignación es 10 minutos; no es necesario llenar los 10 minutos.

## Requisitos de grabación

- Fecha y hora visibles.
- Rostro del estudiante visible.
- Voz audible.
- Demostración, no explicación teórica extensa.
- Mostrar la topología y las pruebas que evidencian el objetivo de seguridad.
- La configuración del FortiGate se presenta mediante GUI.

---

## 0:00–0:35 — Presentación

**Mostrar:** rostro + escritorio + fecha/hora.

**Decir:**

> "Hola, mi nombre es Fred Sneyder Castillo Apolinar, matrícula 2025-2175. En este video voy a demostrar el laboratorio de VPN Site-to-Site de la práctica de Seguridad de Redes.
>
> El objetivo es comunicar un usuario con un servidor mediante una VPN Site-to-Site y comprobar que la comunicación solo funciona cuando el enlace VPN está activo.
>
> La infraestructura utiliza un Cisco 7200 como equipo de red y un FortiGate como peer VPN. La configuración del FortiGate se realizó mediante su interfaz gráfica."

---

## 0:35–1:15 — Topología

**Mostrar:** GNS3 y la topología completa.

**Decir:**

> "En este lado tenemos la red de usuarios, con VLAN 10 y una red 10.21.75.0/25. El gateway de esta red es el Cisco 7200.
>
> El Cisco se conecta mediante el Router-ISP con el FortiGate-B, que protege la red 10.21.75.128/28 donde está el Web Server 10.21.75.130.
>
> Los Browser-PC se utilizan como equipos auxiliares para realizar las pruebas gráficas y acceder al servidor por HTTPS."

---

## 1:15–2:00 — Cisco 7200

**Mostrar:** consola del Cisco.

Mostrar brevemente:

```text
show ip interface brief
show ip route
show crypto map
```

**Decir:**

> "El Cisco 7200 utiliza 203.0.113.21 en su interfaz WAN y 10.21.75.1 en su interfaz LAN.
>
> También proporciona DHCP para la red de usuarios y realiza NAT para la salida general a Internet.
>
> Para el tráfico de la VPN, se utiliza una ACL que identifica la comunicación entre 10.21.75.0/25 y 10.21.75.128/28.
>
> El túnel utiliza IKEv2, DES-SHA256, Diffie-Hellman 14 y PFS con Group 14."

Cuando aparezca `PFS (Y/N): Y`, déjalo visible unos segundos.

---

## 2:00–2:45 — FortiGate-B

**Mostrar:** GUI del FortiGate-B.

Ve a:

`VPN → IPsec Tunnels → VPN-TO-SITE-A`

**Decir:**

> "En FortiGate-B, la interfaz WAN utiliza 203.0.113.26 y la LAN utiliza 10.21.75.129.
>
> El peer remoto es el Cisco con dirección 203.0.113.21.
>
> La VPN utiliza IKEv2 con DES-SHA256 y DH14. En Phase 2 están definidos los selectores entre la red del servidor y la red de usuarios, con PFS habilitado y Group 14."

No muestres ni pronuncies la PSK.

---

## 2:45–3:20 — Policies y NAT

**Mostrar:** `Policy & Objects → Firewall Policy`.

**Decir:**

> "Las políticas de tráfico hacia y desde la VPN mantienen el NAT deshabilitado para conservar las direcciones privadas originales.
>
> Para la salida del Web Server hacia Internet existe una política independiente denominada WEBSERVER_A_INTERNET con NAT habilitado."

No leas todas las columnas.

---

## 3:20–3:50 — VLAN 10 y DHCP

**Mostrar:** Switch-A o evidencia de DHCP del Cisco.

**Decir:**

> "La red de usuarios utiliza VLAN 10. El Cisco 7200 entrega DHCP para la red 10.21.75.0/25 y utiliza 10.21.75.1 como gateway. El rango disponible para clientes es de 10.21.75.10 a 10.21.75.100."

---

## 3:50–4:20 — Web Server y HTTPS

**Mostrar:** Browser-PC con:

`https://10.21.75.130`

**Decir:**

> "El recurso remoto es un servidor Debian con Apache, ubicado en 10.21.75.130/28. Con la VPN activa podemos acceder al servicio HTTPS."

Deja la página visible.

---

## 4:20–4:45 — Estado VPN + ping

**Mostrar primero:** IPsec Monitor del FortiGate con el túnel UP.

Después Browser-PC:

```text
ping 10.21.75.130
```

**Decir:**

> "Con el enlace VPN activo, la comunicación desde el usuario hacia el servidor es exitosa."

---

## 4:45–5:20 — Evidencia IPsec en Cisco

**Mostrar:**

```text
show crypto ikev2 sa
show crypto ipsec sa
```

**Decir:**

> "En el Cisco podemos observar la asociación IKEv2 en estado READY y los contadores de IPsec muestran paquetes encapsulados, cifrados, decapsulados y descifrados. Esto confirma que el tráfico está siendo procesado por el túnel."

---

## 5:20–5:55 — Traceroute

**Mostrar:** consola auxiliar del Browser-PC.

Ejecutar o mostrar el resultado real:

```text
traceroute 10.21.75.130
```

Resultado demostrado en el laboratorio:

```text
1  10.21.75.1
2  * * *
3  10.21.75.130
```

**Decir:**

> "Esta prueba de traceroute muestra el camino desde la red de usuarios hasta el servidor remoto."

---

## 5:55–6:40 — VPN deshabilitada

**Mostrar:**

`Network → Interfaces → VPN-TO-SITE-A`

Deshabilitar administrativamente la interfaz VPN.

Luego volver a Browser-PC:

```text
ping 10.21.75.130
```

**Decir:**

> "Ahora voy a deshabilitar administrativamente la interfaz del túnel VPN, sin apagar el Cisco, el FortiGate ni el servidor.
>
> Voy a repetir exactamente la misma prueba de comunicación."

Cuando falle:

> "La comunicación con el servidor deja de estar disponible. Esto demuestra el comportamiento solicitado por la práctica: el acceso entre las dos redes depende del enlace VPN."

---

## 6:40–7:20 — Restauración

Volver a:

`Network → Interfaces → VPN-TO-SITE-A`

Habilitar nuevamente la interfaz.

Después:

```text
ping 10.21.75.130
```

Y acceder nuevamente al HTTPS si el tiempo lo permite.

**Decir:**

> "Ahora restauro la interfaz del túnel. Después de restablecer la VPN, la comunicación vuelve a funcionar."

---

## 7:20–7:50 — Cierre

**Mostrar:** topología o IPsec Monitor.

**Decir:**

> "Con esto queda demostrado el laboratorio: un Cisco 7200 y un FortiGate establecen una VPN Site-to-Site, el usuario puede comunicarse con el Web Server cuando el túnel está activo, y la comunicación deja de funcionar cuando el túnel se deshabilita.
>
> Soy Fred Sneyder Castillo Apolinar, matrícula 2025-2175. Gracias."
