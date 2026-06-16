# Protocolo SNMP (Puerto 161 UDP)

SNMP monitorea dispositivos de red. Si la comunidad SNMP es debil, puede filtrar mucha informacion del sistema.

> SNMP funciona sobre UDP, por lo que solo se detecta con escaneo UDP (`nmap -sU`).

## Encontrar la Clave de Comunidad SNMP

```bash
onesixtyone -c /usr/share/wordlists/rockyou.txt <IP_objetivo>
```

> `onesixtyone` prueba multiples claves de comunidad (como "public", "private", etc.).

## Enumeracion con snmpwalk

Una vez obtenida la clave, se extrae la informacion del sistema:

```bash
snmpwalk -v 2c -c <clave> <IP_objetivo>
```

- `-v 2c` -> Version del protocolo SNMP
- `-c <clave>` -> Clave de comunidad descubierta
