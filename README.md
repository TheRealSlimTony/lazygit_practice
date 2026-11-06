# Laboratorio guiado de Lazygit

Este repositorio es para aprender Git haciendo, desde Lazygit. No necesitas programar: trabajarás con el menú de una cafetería ficticia. Cada práctica explica **cómo hacerlo** y cómo reconocer el resultado.

## Abrir el laboratorio

En una terminal:

```sh
cd /Users/antoniomendez/Documents/ChatGPT/lazygit_practice
lazygit
```

Ya tienes Lazygit instalado (0.60.0 al preparar este laboratorio). Mantén este README abierto en tu editor mientras practicas. No hay remoto configurado: todo ocurre en tu computadora.

## Antes de empezar: cuatro ideas

- **Directorio de trabajo:** los archivos que editas y todavía no has guardado en un commit.
- **Staging:** los cambios que seleccionaste para el próximo commit. Editar y preparar son pasos distintos.
- **Commit:** una versión guardada, con mensaje e identificador.
- **Rama:** un nombre que apunta a un commit. La rama activa avanza cuando haces un commit; las demás conservan su posición.

`main` es la base. Las ramas `escenario/...` contienen material preparado. Crea tus propias ramas `practica/...` desde ellas para poder repetir las prácticas sin alterar los puntos de partida.

## Cómo moverte

Haz clic en los paneles o usa Tab y las flechas. En **Branches**, busca la pestaña de ramas locales con `[` y `]` si hace falta. `Espacio` cambia a la rama seleccionada; `Enter` muestra sus commits. La rama resaltada por el cursor puede ser distinta de la rama activa: comprueba siempre cuál está activa antes de integrar cambios.

Las mayúsculas cuentan: `M` significa Mayús+m. Pulsa `?` en el panel correspondiente para consultar sus acciones y `Esc` para cerrar. Si tus teclas difieren por configuración, usa la ayuda y el nombre de la acción. Estas son teclas predeterminadas:

| Panel | Tecla | Acción |
| --- | --- | --- |
| Files | Espacio | Preparar o retirar un archivo del staging |
| Files | c | Crear un commit con lo preparado |
| Branches | Espacio | Cambiar a la rama seleccionada |
| Branches | n | Crear una rama desde la seleccionada |
| Branches | M | Integrar la rama seleccionada en la activa |
| Branches | r | Rebasar la rama activa sobre la seleccionada |
| Files | s | Guardar cambios temporalmente en un stash |
| Commits | r | Cambiar el mensaje del commit seleccionado |
| Commits | s | Unir el commit seleccionado con el anterior |
| Cualquier panel | ? / Esc | Consultar ayuda / volver |

## 1. Tu primer commit: editar, revisar y guardar

1. En **Branches**, selecciona `main` y pulsa `Espacio`. Con `main` seleccionada, pulsa `n`, escribe `practica/01-commits` y confirma. Verifica que esta sea la rama activa.
2. En tu editor abre `cafeteria/menu.txt`. Agrega `Chocolate: 1700` y guarda.
3. Vuelve a Lazygit. En **Files**, selecciona el archivo: a la derecha verás la línea agregada. Pulsa `Espacio` para prepararlo.
4. Pulsa `c`, escribe `feat: agregar chocolate al menu` y confirma el formulario siguiendo su pie de ayuda.
5. En **Commits**, selecciona el nuevo commit y pulsa `Enter` para revisar su archivo y su diff.

**Comprueba:** Files queda vacío y el nuevo mensaje aparece arriba de Commits. Cambia a `main`: el chocolate desaparece del archivo. Regresa a `practica/01-commits`: vuelve a aparecer. Cambiar de rama actualiza los archivos a esa versión.

## 2. Dos cambios, dos commits

1. Continúa en `practica/01-commits`. Agrega `Té frío: 1400` a `cafeteria/menu.txt` y una nueva tarea a `cafeteria/tareas.md`.
2. En **Files**, prepara únicamente `menu.txt` con `Espacio`. Pulsa `c` y guarda el mensaje `feat: agregar te frio`.
3. Observa que `tareas.md` sigue pendiente. Prepáralo y crea `docs: actualizar tareas`.

**Comprueba:** hay dos commits nuevos, cada uno con un solo archivo. Staging permite decidir qué cambios viajan juntos.

## 3. Integrar una rama sin conflicto

1. En **Branches**, cambia a `main`. Selecciona `main`, pulsa `n` y crea `practica/03-merge`.
2. Sin cambiar la rama activa, mueve el cursor a `escenario/promocion`.
3. Pulsa `M`, lee el diálogo y confirma la integración en `practica/03-merge`.
4. Abre `cafeteria/promociones.txt` y revisa el historial.

**Comprueba:** aparece la promoción. Puede ser un **fast-forward**: Git solo adelanta el puntero de tu rama porque no hay historias divergentes; no necesita un commit de merge nuevo. `main` conserva su posición.

## 4. Resolver un conflicto de verdad

Dos personas cambiaron el precio del mismo café desde la misma base.

1. En **Branches**, selecciona `escenario/precio-local`, pulsa `n` y crea `practica/04-conflicto`. Verifica que estás en esta nueva rama.
2. Selecciona `escenario/precio-equipo` sin cambiarte a ella. Pulsa `M` y confirma.
3. Git avisará del conflicto. En **Files** selecciona `cafeteria/menu.txt`.
4. Para resolverlo de forma explícita, abre ese archivo en tu editor. Verás un bloque parecido a este:

```text
<<<<<<< HEAD
Café: 1600
=======
Café: 1800
>>>>>>> escenario/precio-equipo
```

5. Sustituye todo ese bloque, incluidas las tres líneas de marcas, por `Café: 1700`. Conserva el resto del menú y guarda.
6. Vuelve a **Files** y prepara `menu.txt` con `Espacio`. Pulsa `m` para abrir las opciones de merge/rebase y elige continuar. Si se solicita mensaje, conserva el propuesto y confirma.

**Comprueba:** no quedan archivos en conflicto; el café cuesta 1700 y el commit de merge tiene dos padres. Puedes ver el grafo con `git log --graph --oneline --all` en otra terminal.

Si quieres cancelar el intento mientras está en curso, pulsa `m` y selecciona abortar el merge; volverás al estado anterior a la integración. Hazlo antes de empezar otra práctica.

## 5. Guardar una interrupción con stash

1. Cambia a `main` y crea `practica/05-stash` con `n`.
2. Agrega `Revisar inventario` a `cafeteria/tareas.md`, guarda, pero no hagas commit.
3. En **Files**, pulsa `s` y escribe una descripción si se solicita. Esto guarda temporalmente tus cambios.
4. Comprueba que Files queda vacío. Cambia a `main` y después regresa a `practica/05-stash`.
5. En el panel **Stash**, selecciona tu entrada, pulsa `?` y ejecuta la acción **Apply** indicada por tu versión. Apply recupera los cambios y conserva la entrada; Pop los recupera y la elimina si tiene éxito.
6. Revisa Files, prepara el archivo y crea `docs: revisar inventario`. Después puedes eliminar la entrada del stash desde su menú, comprobando su descripción.

**Comprueba:** recuperaste la tarea y la guardaste en un commit. Un stash no se recupera automáticamente al regresar a una rama.

## 6. Rebase: colocar tu trabajo sobre una base nueva

1. En **Branches**, selecciona `escenario/rebase-feature`, pulsa `n` y crea `practica/06-rebase`.
2. En **Commits**, observa los dos commits `feat: agregar horario...` y `docs: ampliar horario...`. Opcionalmente anota sus identificadores.
3. En **Branches**, selecciona `escenario/rebase-base` sin cambiarte a ella. Pulsa `r`, revisa que la operación sea rebasar tu rama activa sobre esa base y confirma.
4. Revisa el historial y los archivos `cafeteria/horarios.txt` y `cafeteria/contacto.txt`.

**Comprueba:** tus dos commits están ahora encima de `chore: agregar contacto de cafeteria`; sus identificadores cambiaron y los archivos de ambas ramas están presentes. Rebase vuelve a crear tus commits sobre otra base. Aquí trabajas con copias locales propias.

## 7. Limpiar dos commits con squash

1. Selecciona `escenario/rebase-feature` y crea `practica/07-squash` con `n`.
2. En **Commits**, selecciona el más reciente: `docs: ampliar horario de fin de semana`.
3. Pulsa `s` para unirlo con el commit inmediatamente anterior, `feat: agregar horario de cafeteria`. Confirma los diálogos; si aparece un editor de mensaje, escribe `feat: definir horarios de cafeteria`, guarda y cierra.
4. Si necesitas ajustar el mensaje después, selecciona el commit resultante y usa `r`.

**Comprueba:** los dos commits del horario se convirtieron en uno y `cafeteria/horarios.txt` conserva las dos líneas. Squash cambia el historial, no el contenido final.

## 8. Traer solo un commit con cherry-pick

1. Cambia a `escenario/promocion`. En **Commits**, selecciona `feat: agregar promocion de desayuno` y pulsa `C` (Mayús+c) para marcarlo.
2. En **Branches**, cambia a `main`, selecciona `main` y crea `practica/08-cherry-pick` con `n`.
3. En **Commits**, pulsa `V` (Mayús+v) para aplicar el commit marcado y confirma.

**Comprueba:** tu rama contiene la promoción sin integrar otras ramas enteras. Cherry-pick aplica el cambio de un commit en la rama activa; su identificador puede ser diferente.

## Repetir y orientarte

Antes de cambiar de ejercicio, deja **Files** vacío y termina o aborta cualquier merge/rebase en curso. Puedes guardar pendientes con un commit o stash. Para repetir, crea otra rama desde el mismo punto de partida, por ejemplo `practica/04-conflicto-intento-2`. Las ramas `escenario/...` y las etiquetas `inicio/...` conservan las versiones originales si sigues la guía.

Comandos de consulta opcionales desde otra terminal:

```sh
git status                     # Rama activa y cambios pendientes
git log --graph --oneline --all # Todas las historias
git diff                       # Cambios sin preparar
git diff --staged               # Lo que entraría en el próximo commit
```

No necesitas usar reset ni borrar ramas para repetir. Si una acción te desconcierta, cancela el diálogo con `Esc`, revisa `git status` y consulta `?` en el panel. No uses “descartar cambios” para guardar trabajo: esa acción elimina ediciones pendientes.

## Mapa de puntos de partida

| Práctica | Crear tu rama desde | Otra rama que seleccionas para integrar |
| --- | --- | --- |
| 1 y 2: commits | main | — |
| 3: merge | main | escenario/promocion |
| 4: conflicto | escenario/precio-local | escenario/precio-equipo |
| 5: stash | main | — |
| 6: rebase | escenario/rebase-feature | escenario/rebase-base |
| 7: squash | escenario/rebase-feature | — |
| 8: cherry-pick | main | Copiar primero el commit de escenario/promocion |

Referencia de teclas: [documentación oficial de Lazygit](https://github.com/jesseduffield/lazygit/blob/master/docs/keybindings/Keybindings_en.md). La ayuda `?` de tu instalación es la referencia inmediata para cada panel.
