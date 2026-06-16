# Wireshark: Interceptacion de Credenciales

Wireshark captura trafico de red. En protocolos no seguros, las credenciales viajan en texto plano.

## Captura de Trafico

1. Seleccionar interfaz de red (Ethernet, Wi-Fi)
2. Click en **Start** para comenzar la captura
3. Estar en la misma red que la victima

## Filtros para Protocolos Vulnerables

| Protocolo | Filtro Wireshark    |
| --------- | ------------------- |
| HTTP      | `http`              |
| FTP       | `ftp`               |
| Telnet    | `telnet`            |
| POP3      | `pop`               |
| IMAP      | `imap`              |

## Donde Buscar las Credenciales

- **HTTP**: Buscar paquetes `POST` con parametros `username` y `password`
- **FTP**: Buscar lineas que contengan `USER` y `PASS`
- **Telnet**: Las credenciales aparecen al inicio de la comunicacion
- **POP3/IMAP**: Comandos `USER` y `PASS` en los paquetes

## Lectura de Paquetes

Seleccionar un paquete y expandir en la seccion inferior **Packet Details** las capas del protocolo. Los datos sensibles aparecen en texto claro.
