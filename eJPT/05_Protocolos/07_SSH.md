## Acceso al servicio SSH

```
ssh <nombre>@<IP_objetivo>
```

ssh -i id_rsa john@10.129.12.10

## Acceso al servicio FTP

```
ftp <nombre>@<IP_objetivo>
```
#### FTP

- Access and Environment
- Anonymous FTP access was enabled on port 21
- We identified this as a home directory for user `john`
- Several important configuration and history files were accessible

#### Critical Files

- `.bash_history` file revealed potential credentials: john:SuperSecurePass123
- SSH private key (`id_rsa`) was obtained and is not password protected

put
instalas 

get 
descargas

find / -name id_rsa 2>/dev/null
