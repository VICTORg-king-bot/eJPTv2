# Escaneo con Nmap

Nmap es la herramienta principal para descubrir puertos y servicios en los hosts objetivo.

## Escaneo Basico

```bash
nmap <IP_objetivo>
```

## Escaneo Completo (Recomendado para eJPT)

Escanea todos los puertos TCP, detecta versiones de servicios y aplica scripts por defecto. Para el examen se recomienda reducir `--min-rate` a 2000 para evitar deteccion.

```bash
nmap -p- --open -sS -sC -sV --min-rate 5000 -n -vvv -Pn <IP_objetivo> -oN escaneo
```

```bash
nmap -sn <IP>/24
sudo nmap -sS --min-rate 5000 -p- --open -Pn <IP> -oN tcp_scan.txt
grep '^[0-9]' tcp_scan.txt | cut -d '/' -f1 | sort -u | xargs | tr ' ' ','
nmap -sC -sV --open -Pn <IP> -oN Full_scan.txt
```

**Parámetros explicados:**
- `-p-` -> Escanea todos los 65535 puertos TCP
- `--open` -> Muestra solo puertos abiertos
- `-sS` -> Escaneo SYN (sigiloso, half-open)
- `-sC` -> Ejecuta scripts NSE por defecto (enumeración básica)
- `-sV` -> Detecta versión de los servicios
- `--min-rate 5000` -> Mínimo 5000 paquetes/segundo (acelera el escaneo)
- `-n` -> No resuelve DNS (más rápido)
- `-vvv` -> Verbosidad alta (ver resultados en tiempo real)
- `-Pn` -> Omite deteccion por ping (asume que el host esta activo)
- `-oN escaneo` -> Guarda el resultado en un archivo de texto

## Escaneo de Vulnerabilidades con Nmap

Nmap dispone de scripts para detectar vulnerabilidades conocidas en los servicios:

```bash
nmap --script "vuln" -p<puerto> <IP_objetivo>
```

```bash
nmap --script "smb-vuln-*" -p<puerto> <IP_objetivo>
```
## Escaneo de Puertos UDP

Por defecto Nmap solo escanea TCP. Para descubrir servicios UDP como SNMP o DNS:

```bash
nmap -sU --top-ports 200 --min-rate=5000 -Pn <IP_objetivo>
```

> `--top-ports 200` escanea los 200 puertos UDP más comunes.
