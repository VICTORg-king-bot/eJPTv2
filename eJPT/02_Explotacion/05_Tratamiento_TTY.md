# Tratamiento de la TTY

Al recibir una reverse shell, la terminal suele ser limitada (sin tabulación, sin historial, etc.). Estos comandos la vuelven interactiva y funcional.

## Procedimiento Estándar

```bash
script /dev/null -c bash
# Presionar Ctrl+Z para suspender la sesión
```

En nuestra máquina atacante:

```bash
stty raw -echo; fg
```

Al recuperar la sesion:

```bash
reset xterm
export TERM=xterm
export SHELL=bash
```

**Explicación paso a paso:**
1. `script /dev/null -c bash` -> Crea una nueva terminal dentro de la sesión actual
2. `Ctrl+Z` -> Suspende la sesión para ajustar la terminal local
3. `stty raw -echo; fg` -> Desactiva el eco local y reanuda la sesión
4. `reset xterm` -> Resetea la terminal con formato xterm
5. `export TERM=xterm` -> Define el tipo de terminal (permite colores y limpieza)
6. `export SHELL=bash` -> Define la shell como bash

## Alternativa con Python

Si Python está disponible en la víctima, se puede usar para mejorar la TTY:

```bash
python3 -c 'import pty; pty.spawn("/bin/bash")'
```

Después, en la máquina atacante:

```bash
stty raw -echo; fg
reset xterm
export TERM=xterm
export SHELL=bash
```

### Ajustar Tamaño de la Terminal

En la máquina atacante, verificar el tamaño actual:

```bash
stty size
```

Luego, después de `reset xterm`, ajustar las dimensiones:

```bash
stty rows <filas> cols <columnas>
```