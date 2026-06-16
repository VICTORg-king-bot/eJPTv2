# Protocolo RDP (Puerto 3389)

RDP permite acceso remoto al escritorio de Windows.

## Conexion con xfreerdp

```bash
xfreerdp /u:<Administrator> /p:<contraseña> /v:<IP_objetivo>:3389
```

## Enumeracion Basica del Sistema Windows

Una vez dentro del sistema (via RDP o shell), estos comandos revelan informacion del sistema.

### Listar Usuarios

```cmd
net user
```

### Informacion de un Usuario Especifico

```cmd
net user <nombre_usuario>
```

### Ver Grupos Locales

```cmd
net localgroup Administrators
```

hydra -l j <john> -p <"SuperSecurePass123"> rdp://10.129.12.20