# Fuzzing Web: Descubrimiento de Directorios y Archivos

El fuzzing web permite descubrir rutas, archivos y directorios ocultos en un servidor web.

## Gobuster

```bash
gobuster dir -u http://<IP>/ -w /usr/share/wordlists/seclists/Discovery/Web-Content/DirBuster-2007_directory-list-lowercase-2.3-medium.txt  -x txt,py,php,sh
```

> `-x` especifica extensiones a buscar (php, txt, etc.)

## Wfuzz

```bash
wfuzz -c --hc 404 -w /usr/share/wordlists/seclists/Discovery/Web-Content/DirBuster-2007_directory-list-lowercase-2.3-medium.txt  http://<IP>/FUZZ
```

> `--hc 404` oculta las respuestas con código 404 (no encontrado).
> `FUZZ` es la palabra clave que wfuzz reemplaza con cada elemento del diccionario.
> `--hl 368` oculta las respuestas con 368 líneas.

## Dirb

```bash
dirb http://<IP>
```

## Dirsearch

```bash
dirsearch -u http://<IP>/ -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-lowercase-2.3-medium.txt
```

> Dirsearch es más moderno y por defecto ya busca extensiones comunes.
