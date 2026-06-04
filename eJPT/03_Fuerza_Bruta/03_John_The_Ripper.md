# John The Ripper: Fuerza Bruta en Local

Se usa para romper hashes y archivos cifrados (ZIP, PDF, Keepass, claves SSH, etc.).

## Archivos ZIP Protegidos con Contrasena

```bash
zip2john archivo.zip > hash
john --wordlist=/usr/share/wordlists/rockyou.txt hash
```

## Archivos Keepass (.kdbx)

```bash
keepass2john Database.kdbx > hash
john --wordlist=/usr/share/wordlists/rockyou.txt hash
```

## Claves Privadas SSH (id_rsa)

Cuando una clave SSH tiene contrasena, se convierte a hash con ssh2john y se crackea.

```bash
ssh2john id_rsa > hash
john --wordlist=/usr/share/wordlists/rockyou.txt hash
```

## Hashes Directos

Se identifica el tipo de hash con `hash-identifier` y se pasa el formato a john.

```bash
hash-identifier
```

```bash
john --format=<RAW-MD5> --wordlist=/usr/share/wordlists/rockyou.txt hash
```
