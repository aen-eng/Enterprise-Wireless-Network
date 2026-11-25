
from pathlib import Path
import zipfile

base = Path("/mnt/data/LAB12_Enterprise_Wireless_Network")
readme_path = base / "README.md"

readme = """# LAB12 — Enterprise Wireless Network

## Objetivo

Implementar una red inalámbrica empresarial en Cisco Packet Tracer utilizando:

- Cisco WLC
- Lightweight AP
- VLANs
- Trunks 802.1Q
- Router-on-a-Stick
- DHCP
- WPA2-Personal
- WPA2-Enterprise
- RADIUS / 802.1X

Durante las pruebas, los clientes inalámbricos lograron autenticarse correctamente, pero recibieron direcciones IP de la VLAN de management en lugar de las VLAN asignadas a cada WLAN.

El laboratorio terminó convirtiéndose también en una práctica de troubleshooting.

---

## Topología

![Topología del laboratorio](images/wireless-no-8021q-tag.png)

> En el repositorio puede reemplazarse esta imagen por la captura completa de la topología de Packet Tracer.

---

## VLANs

| VLAN | Función | Subred |
|---:|---|---|
| 10 | Management | 192.168.10.0/24 |
| 20 | WIFI-USERS | 192.168.20.0/24 |
| 30 | WIFI-CORP | 192.168.30.0/24 |
| 40 | AAA / RADIUS | 192.168.40.0/24 |

---

## Wireless

### WIFI-USERS

- VLAN 20
- WPA2-Personal
- AES
- PSK configurada localmente

### WIFI-CORP

- VLAN 30
- WPA2-Enterprise
- AES
- 802.1X
- RADIUS

La autenticación Enterprise fue probada con credenciales correctas e incorrectas.

---

## Credenciales

Las contraseñas, PSK y shared secrets utilizados en el laboratorio no se publican en el repositorio.

```text
WLC Password: [REDACTED]
WIFI-USERS PSK: [REDACTED]
RADIUS Shared Secret: [REDACTED]

802.1X Test User: corpuser
Password: [REDACTED]
```

---

## Problema encontrado

Los clientes inalámbricos se autenticaban correctamente, pero obtenían direcciones IP de la VLAN 10 en lugar de sus VLAN correspondientes.

Comportamiento esperado:

```text
WIFI-USERS -> VLAN 20
WIFI-CORP  -> VLAN 30
```

Comportamiento observado:

```text
Wireless clients -> VLAN 10
```

---

## Troubleshooting realizado

Se verificó:

- configuración de trunks;
- interfaces dinámicas del WLC;
- mapeo WLAN-VLAN;
- Router-on-a-Stick;
- DHCP;
- tablas MAC;
- tráfico en Simulation Mode;
- presencia de etiquetas 802.1Q.

La red cableada funcionó correctamente.

En las pruebas de tráfico cableado se observó el encabezado 802.1Q esperado.

![Tráfico con etiqueta 802.1Q](images/wired-8021q-tagged.png)

En el tráfico inalámbrico inspeccionado no se observó el mismo comportamiento esperado de etiquetado.

---

## Resultado

- [x] AP registrado
- [x] CAPWAP operativo
- [x] WPA2-Personal
- [x] WPA2-Enterprise
- [x] RADIUS / 802.1X
- [x] DHCP cableado
- [x] Router-on-a-Stick
- [x] Troubleshooting con Simulation Mode
- [x] Análisis de tablas MAC
- [ ] Segmentación inalámbrica resuelta

---

## Conclusión

El laboratorio permitió comprobar que autenticación y segmentación son procesos diferentes.

Aunque WPA2 y RADIUS funcionaron correctamente, la asignación de VLAN de los clientes inalámbricos no se comportó como se esperaba.

La evidencia obtenida sugiere un posible comportamiento o limitación de Cisco Packet Tracer relacionado con la segmentación VLAN inalámbrica, pero la causa definitiva no fue confirmada.

Por ese motivo, el problema se documenta como **no resuelto**, evitando asumir una causa sin evidencia suficiente.

---

## Entorno

- Cisco Packet Tracer 9.0.0.0810
- Fecha: noviembre de 2026
- Estado: Authentication Validated / VLAN Segmentation Unresolved
"""

readme_path.write_text(readme, encoding="utf-8")

zip_path = Path("/mnt/data/LAB12_Enterprise_Wireless_Network_GitHub_simple.zip")
with zipfile.ZipFile(zip_path, "w", zipfile.ZIP_DEFLATED) as z:
    for p in base.rglob("*"):
        if p.is_file():
            z.write(p, p.relative_to(base))

print(readme_path)
print(zip_path)
