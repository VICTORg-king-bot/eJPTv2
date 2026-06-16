# Puertos y Servicios Comunes

Conocer los puertos por defecto ayuda a identificar rápidamente qué servicios están corriendo en el objetivo.

## Protocolos TCP

| Puerto | Servicio   | Descripcion                      |
| ------ | ---------- | -------------------------------- |
| 21     | FTP        | Transferencia de archivos        |
| 22     | SSH        | Shell seguro (acceso remoto)     |
| 23     | Telnet     | Shell sin cifrar (inseguro)      |
| 25     | SMTP       | Envio de correo                  |
| 53     | DNS        | Resolucion de nombres            |
| 80     | HTTP       | Web sin cifrar                   |
| 110    | POP3       | Recepcion de correo              |
| 135    | RPC        | Llamadas a procedimiento remoto  |
| 139    | NetBIOS    | Comparticion de archivos (SMB)   |
| 143    | IMAP       | Correo electronico               |
| 443    | HTTPS      | Web cifrada                      |
| 445    | SMB        | Comparticion de archivos Windows |
| 3306   | MySQL      | Base de datos MySQL              |
| 3389   | RDP        | Escritorio remoto Windows        |
| 8080   | HTTP-Proxy | Servidor web alternativo         |

## Protocolos UDP

| Puerto | Servicio | Descripcion                      |
| ------ | -------- | -------------------------------- |
| 53     | DNS      | Resolucion de nombres            |
| 67     | DHCP     | Asignacion de IP                 |
| 68     | DHCP     | Asignacion de IP                 |
| 69     | TFTP     | Transferencia de archivos simple |
| 161    | SNMP     | Monitoreo de red                 |

> SNMP es especialmente importante porque puede filtrar información del sistema si la comunidad es pública o débil.
