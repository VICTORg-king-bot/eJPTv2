# Protocolo RDP (Puerto 3389)

RDP permite acceso remoto al escritorio de Windows.

## Conexión con xfreerdp

```bash
xfreerdp /u:<Administrator> /p:<contraseña> /v:<IP_objetivo>:3389
```

## Enumeración Básica del Sistema Windows

Una vez dentro del sistema (vía RDP o shell), estos comandos revelan información del sistema.

### Listar Usuarios

```cmd
net user
```

### Información de un Usuario Específico

```cmd
net user <nombre_usuario>
```

### Ver Grupos Locales

```cmd
net localgroup Administrators
```