# Enumeracion de Usuarios en Windows

Una vez dentro de un sistema Windows, enumerar usuarios ayuda a identificar objetivos para escalada.

## Listar Usuarios del Sistema

```cmd
net users
```

## Informacion de un Usuario Especifico

```cmd
net user <nombre_usuario>
```

## Ver Miembros del Grupo Administradores

```cmd
net localgroup Administrators
```

## Enumeracion desde Meterpreter

Con una sesion de meterpreter activa:

```bash
shell
net users
```
