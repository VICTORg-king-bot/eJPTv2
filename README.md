# eJPTv2: Apuntes para la Certificación

Apuntes organizados para la preparación del examen **eJPTv2 (eLearnSecurity Junior Penetration Tester)**.

## Fuentes principales

- Curso *"eJPTv2: Directo a la Certificación"* de [El Rincón del Hacker](https://elrincondelhacker.es/).
- 🧪 *Laboratorio de preparación eJPTv2* | Simulación de examen de [Xerosec: ](https://www.youtube.com/watch?v=v20IsEd5nUU&t=15325s ). 
- *Junior Cybersecurity Analyst Path* de [Hack The Box Academy](https://academy.hackthebox.com/path/preview/junior-cybersecurity-analyst).
- Documentación oficial y laboratorios prácticos.
- Notas y experiencia personal durante el estudio.

El objetivo de estos apuntes es servir como guía de consulta rápida y material de repaso para los temas cubiertos en la certificación eJPTv2.

## Estructura

```
eJPT/
├── 01_Reconocimiento/           # Descubrimiento de red, Nmap, puertos
├── 02_Explotacion/              # Reverse shells, msfvenom, Metasploit, TTY
├── 03_Fuerza_Bruta/             # Hydra, john, Metasploit, bases de datos
├── 04_Vulnerabilidades_Web/     # Fuzzing, LFI, SQLi, file upload, webshells
├── 05_Protocolos/               # SMB, SNMP, RDP, IIS, SAMBA
├── 06_CMS/                      # WordPress, Drupal
├── 07_Escalada_de_Privilegios/  # SUID, sudo, Windows, local_exploit_suggester
└── 08_Pivoting/                 # Metasploit autoroute, SSHuttle, port forwarding
```

## Contenido

| Carpeta | Descripcion |
|---------|-------------|
| `01_Reconocimiento` | Escaneo de red (arp-scan, netdiscover), Nmap (TCP/UDP, scripts vuln), tabla de puertos y servicios |
| `02_Explotacion` | Reverse shells con netcat, transferencia de archivos, generacion de payloads con msfvenom, uso de Metasploit (multi/handler, EternalBlue, vsftpd), tratamiento de TTY |
| `03_Fuerza_Bruta` | Hydra (SSH, FTP, HTTP, MySQL), módulos de Metasploit (smb_login, ssh_login, ftp_login), John The Ripper (zip, keepass, ssh2john, hashes) |
| `04_Vulnerabilidades_Web` | Fuzzing (gobuster, wfuzz, dirb, dirsearch), LFI, SQL injection con SQLmap, file upload y bypass, webshells, subdominios y transferencia DNS, captura de credenciales con Wireshark, Tomcat |
| `05_Protocolos` | SMB (smbclient, smbmap, psexec), SAMBA/RPCClient, SNMP (onesixtyone, snmpwalk), RDP (xfreerdp), IIS (webshell ASPX), hotfixes Windows |
| `06_CMS` | WordPress (WPScan, fuerza bruta, reverse shell), Drupal (Drupalgeddon, settings.php) |
| `07_Escalada_de_Privilegios` | Binarios SUID (GTFOBins), sudo -l, enumeracion de usuarios Windows, local_exploit_suggester |
| `08_Pivoting` | Autoroute + port forwarding con Metasploit, SSHuttle, portproxy en Windows |

## Herramientas Cubiertas

`nmap` `arp-scan` `netdiscover` `netcat` `msfvenom` `Metasploit` `hydra` `john` `sqlmap` `gobuster` `wfuzz` `dirb` `dirsearch` `wpscan` `smbclient` `smbmap` `rpcclient` `snmpwalk` `onesixtyone` `xfreerdp` `sshuttle` `impacket` `wireshark` `whatweb` `crackmapexec` `nikto`

## Nota

Estos apuntes están pensados como guía de consulta rápida durante el estudio y el examen. Incluyen comandos con parámetros explicados y pequeños contextos para recordar el propósito de cada técnica.
