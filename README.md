
# 📡 LAB12 — Enterprise Wireless Network

**Cisco WLC | WPA2 | RADIUS | Network Troubleshooting**

![Cisco](https://img.shields.io/badge/Cisco-Networking-049FD9)
![Wireless](https://img.shields.io/badge/Wireless-WPA2-blue)
![Security](https://img.shields.io/badge/Security-802.1X-green)

## 🎯 Descripción

Implementación de una infraestructura inalámbrica empresarial
centralizada mediante Cisco WLC y Lightweight AP, integrando
segmentación VLAN, DHCP y autenticación RADIUS.

## ⚙️ Tecnologías implementadas

- Wireless LAN Controller (WLC).
- Lightweight AP y CAPWAP.
- WPA2-Personal y WPA2-Enterprise.
- AAA, RADIUS e IEEE 802.1X.
- VLANs y trunks 802.1Q.
- Router-on-a-Stick y DHCP.

## 🌐 Segmentación de red

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
con credenciales correctas e incorrectas.

## 🔍 Troubleshooting

Durante las pruebas, ambos clientes inalámbricos recibieron
direcciones IP de la VLAN 10 en lugar de las VLANs 20 y 30.

Para investigar este comportamiento se utilizaron:

- Verificación de trunks e interfaces dinámicas.
- Análisis de tablas MAC.
- Pruebas de conectividad y DHCP.
- Inspección de tramas Ethernet en Simulation Mode.

### Evidencia técnica

| Verificación | Cableado | Inalámbrico |
|---|:---:|:---:|
| Etiquetado 802.1Q visible | ✅ | ❌ |
| Clasificación VLAN correcta | ✅ | ❌ |
| DHCP en subred esperada | ✅ | ❌ |

La evidencia apunta a una posible limitación del etiquetado
802.1Q en el WLC simulado, sin confirmación oficial de un bug.

## 📊 Resultados

- [x] Registro del AP y comunicación CAPWAP.
- [x] WPA2-Personal.
- [x] WPA2-Enterprise y autenticación RADIUS.
- [x] Routing y DHCP cableado.
- [x] Análisis de tráfico y troubleshooting.
- [ ] Segmentación inalámbrica efectiva.

## 💡 Conclusión

El proyecto permitió reforzar la implementación de redes
Wireless empresariales y el diagnóstico de problemas de
conectividad mediante evidencia técnica, diferenciando
la autenticación de la segmentación del tráfico.

---

**Environment:** Cisco Packet Tracer 9.0.0.0810

**Status:** Authentication Validated | VLAN Segmentation Unresolved

**Date:** November 2026
