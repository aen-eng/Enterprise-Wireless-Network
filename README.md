
# 📡 LAB12 — Enterprise Wireless Network

**Cisco WLC | WPA2 | RADIUS | Network Troubleshooting**

![Cisco](https://img.shields.io/badge/Cisco-Networking-049FD9)
![Wireless](https://img.shields.io/badge/Wireless-WPA2-blue)
![Security](https://img.shields.io/badge/Security-802.1X-green)

## 🎯 Objetivo y desafío

El objetivo inicial de este laboratorio fue implementar una
infraestructura inalámbrica empresarial centralizada, utilizando
Cisco WLC, Lightweight AP, segmentación mediante VLANs y
autenticación WPA2-Personal y WPA2-Enterprise.

Durante la implementación, a pesar de verificar las
configuraciones, se detectó un comportamiento inesperado
en el etiquetado 802.1Q del tráfico inalámbrico.

Esta situación transformó el laboratorio en una oportunidad
para profundizar en el análisis de tráfico, investigar las
posibles limitaciones del simulador y desarrollar una
metodología de troubleshooting basada en evidencia.

## ⚙️ Tecnologías implementadas

- Wireless LAN Controller (WLC).
- Lightweight AP y CAPWAP.
- WPA2-Personal y WPA2-Enterprise.
- AAA, RADIUS e IEEE 802.1X.
- VLANs y trunks 802.1Q.
- Router-on-a-Stick y DHCP.

## 🌐 Diseño de red

| VLAN | Función | Subred |
|---|---|---|
| 10 | Management | 192.168.10.0/24 |
| 20 | WIFI-USERS | 192.168.20.0/24 |
| 30 | WIFI-CORP | 192.168.30.0/24 |
| 40 | AAA Services | 192.168.40.0/24 |

## 🔐 Seguridad Wireless

| Configuración | WPA2-Personal | WPA2-Enterprise |
|---|:---:|:---:|
| SSID | WIFI-USERS | WIFI-CORP |
| VLAN | 20 | 30 |
| WPA2 | ✅ | ✅ |
| AES | ✅ | ✅ |
| TKIP | ⬜ | ⬜ |
| PSK | ✅ | ⬜ |
| 802.1X | ⬜ | ✅ |
| RADIUS | ⬜ | ✅ |

La autenticación Enterprise se validó mediante pruebas
con credenciales correctas e incorrectas, comprobando
el rechazo y la recuperación de la conexión.

## 🔍 Investigación y troubleshooting

Los clientes inalámbricos se autenticaban correctamente,
pero obtenían direcciones IP de la VLAN de management
en lugar de las VLANs asignadas a sus respectivas WLAN.

Para identificar el origen del problema se realizaron:

- Verificación de trunks e interfaces dinámicas del WLC.
- Validación de routing y DHCP mediante tráfico cableado.
- Análisis de tablas de direcciones MAC.
- Inspección de encabezados Ethernet en Simulation Mode.
- Comparación del etiquetado 802.1Q entre ambos escenarios.

### Evidencia obtenida

| Verificación | Cableado | Inalámbrico |
|---|:---:|:---:|
| Etiquetado 802.1Q visible | ✅ | ❌ |
| Clasificación VLAN correcta | ✅ | ❌ |
| DHCP en subred esperada | ✅ | ❌ |

Las direcciones MAC de ambos clientes inalámbricos fueron
aprendidas en la VLAN nativa 10 a través del puerto
conectado al WLC.

La evidencia apunta a una posible limitación del
etiquetado 802.1Q en Packet Tracer, aunque su causa
definitiva permanece sin confirmar.

## 📊 Resultados

- [x] Registro del AP y comunicación CAPWAP.
- [x] WPA2-Personal.
- [x] WPA2-Enterprise y autenticación RADIUS.
- [x] Routing y DHCP cableado.
- [x] Análisis de tráfico y aislamiento del problema.
- [ ] Segmentación inalámbrica efectiva.

## 💡 Aprendizaje y reflexión

No todos los desafíos técnicos se resuelven modificando
una configuración. En ocasiones, las limitaciones de
una herramienta obligan a investigar más allá de lo
esperado.

Este laboratorio permitió profundizar en el funcionamiento
del tráfico inalámbrico, diferenciar los problemas de
autenticación de los de segmentación y fundamentar
cada diagnóstico mediante evidencia técnica.

El valor del proyecto no reside únicamente en configurar
una infraestructura, sino también en comprender su
comportamiento, cuestionar los resultados y desarrollar
criterio técnico frente a situaciones inesperadas.

---

**Environment:** Cisco Packet Tracer 9.0.0.0810

**Status:** Authentication Validated | VLAN Segmentation Unresolved

**Date:** November 2026
