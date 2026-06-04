# Tratamiento de la TTY

Al recibir una reverse shell, la terminal suele ser limitada (sin tabulación, sin historial, etc.). Estos comandos la vuelven interactiva y funcional.

## Procedimiento Estandar

```bash
script /dev/null -c bash
# Presionar Ctrl+Z para suspender la sesion
```

En nuestra maquina atacante:

```bash
stty raw -echo; fg
```

Al recuperar la sesion:

```bash
reset xterm
export TERM=xterm
export SHELL=bash
```

**Explicacion paso a paso:**
1. `script /dev/null -c bash` -> Crea una nueva terminal dentro de la sesion actual
2. `Ctrl+Z` -> Suspende la sesion para ajustar la terminal local
3. `stty raw -echo; fg` -> Desactiva el eco local y reanuda la sesion
4. `reset xterm` -> Resetea la terminal con formato xterm
5. `export TERM=xterm` -> Define el tipo de terminal (permite colores y limpieza)
6. `export SHELL=bash` -> Define la shell como bash
