# Enumeracion de Subdominios y Ataque de Transferencia de Zona DNS

## Configurar /etc/hosts

Antes de trabajar con dominios, se asocia la IP al nombre de dominio en el archivo local:

```bash
sudo nano /etc/hosts
<IP_objetivo> <dominio>
```

> Esto evita depender de DNS externos y permite resolver el dominio localmente.

## Ataque de Transferencia de Zona DNS

Si el puerto 53 (DNS) esta abierto, se puede intentar obtener todos los registros DNS del dominio:

```bash
dig axfr <dominio> @<IP_objetivo>
```

> Si el servidor DNS permite transferencia de zona, obtendremos todos los subdominios.

## Enumeracion de Subdominios con Wfuzz

Se fuerza la busqueda de subdominios usando un diccionario:

```bash
wfuzz -c --hc=404 --hl=1 \
  -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-110000.txt \
  -H "Host: FUZZ.<dominio>" \
  -u <IP_objetivo>
```

```bash
wfuzz -c --hc=404 --hl=367 \
  -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-20000.txt \
  -H "Host: FUZZ.<dominio>" \
  -u <IP_objetivo>
```

> `--hl` oculta respuestas con un numero especifico de lineas (ayuda a filtrar falsos positivos).

## Uso de /etc/hosts con Subdominios Descubiertos

Cada subdominio valido se agrega al `/etc/hosts`:

```
<IP> <dominio> <subdominio.<dominio>>
```
