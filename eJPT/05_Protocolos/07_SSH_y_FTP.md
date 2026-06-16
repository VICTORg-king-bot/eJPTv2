# Protocolo SSH (Puerto 22)

SSH permite acceso remoto seguro a sistemas Linux/Unix.

## Acceso al Servicio SSH

```bash
ssh <usuario>@<IP_objetivo>
```

### Usar Clave Privada id_rsa

```bash
ssh -i id_rsa <usuario>@<IP_objetivo>
```

### Buscar Claves id_rsa en el Sistema

```bash
find / -name id_rsa 2>/dev/null
```

## Transferencia de Archivos con SCP

```bash
# Subir archivo
scp <archivo> <usuario>@<IP_objetivo>:/ruta/destino

# Descargar archivo
scp <usuario>@<IP_objetivo>:/ruta/origen <archivo>
```

## Protocolo FTP (Puerto 21)

FTP transfiere archivos sin cifrado. Las credenciales viajan en texto plano.

### Acceso al Servicio FTP

```bash
ftp <usuario>@<IP_objetivo>
```

### Comandos Básicos de FTP

| Comando | Descripción                      |
| ------- | -------------------------------- |
| `put`   | Sube un archivo al servidor      |
| `get`   | Descarga un archivo del servidor |
