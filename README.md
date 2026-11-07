# Laboratorio guiado de Lazygit

Este repositorio es para aprender Git haciendo, desde Lazygit. No necesitas programar: trabajarás con el menú de una cafetería ficticia. Cada práctica explica **cómo hacerlo** y cómo reconocer el resultado.

## Abrir el laboratorio

En una terminal:

```sh
cd /Users/antoniomendez/Documents/GitHub/lazygit_practice
lazygit
```

Ya tienes Lazygit instalado (0.60.0 al preparar este laboratorio). Mantén este README abierto en tu editor mientras practicas. No hay remoto configurado: todo ocurre en tu computadora.

## Antes de empezar: conceptos

- **Directorio de trabajo:** los archivos que editas y todavía no has guardado en un commit.
- **Staging:** los cambios que seleccionaste para el próximo commit. Editar y preparar son pasos distintos.
- **Commit:** una versión guardada, con mensaje e identificador.
- **Rama:** un nombre que apunta a un commit. La rama activa avanza cuando haces un commit; las demás conservan su posición.

- **HEAD:** señala la versión en la que estás trabajando; normalmente apunta a tu rama activa.
- **Diff:** comparación entre versiones; las líneas agregadas y eliminadas muestran el cambio.
- **Merge:** integra otra rama en la activa. Si ambas avanzaron desde la base común, el commit de merge conecta las dos historias mediante dos padres.
- **Fast-forward:** cuando tu rama es antecesora de la otra, basta adelantar su puntero. No hace falta recrear commits.
- **Conflicto:** Git necesita que elijas el contenido final porque dos cambios se superponen. No significa que hayas perdido el trabajo.
- **Rebase:** vuelve a crear los commits de tu rama sobre otra base. Cambian sus identificadores; evita hacerlo con historia compartida sin coordinarlo.
- **Squash:** combina varios cambios en un solo commit.
- **Stash:** guarda temporalmente ediciones pendientes; no sustituye un commit definitivo.
- **Cherry-pick:** aplica el cambio de un commit concreto sobre tu rama activa.
- **Etiqueta (tag):** nombre fijo para una versión. Las etiquetas `inicio/...` son los puntos de restauración del laboratorio.

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

## Qué elegir en el menú de merge

Al pulsar `M` en Branches, usa las flechas para seleccionar la opción y `Enter` para aceptarla. Si aparece una confirmación adicional, revisa los nombres de origen y destino, elige **Confirm / Yes** y pulsa `Enter`. La rama activa es siempre el destino; la seleccionada es el origen.

| Opción del menú | Qué significa | Uso aquí |
| --- | --- | --- |
| **Regular Merge** | Integra conservando las historias. Normalmente crea un commit de merge incluso si sería posible adelantar el puntero (`--no-ff`). | **Ejercicio 4**, para unir historias divergentes y resolver su conflicto. |
| **Regular Merge (fast-forward)** | Permite adelantar el puntero si es posible. Si las ramas divergieron, puede hacer un merge normal; no significa necesariamente “solo fast-forward”. | **Ejercicio 3**, donde sí es posible adelantarlo. |
| **Squash Merge (uncommitted)** | Combina el resultado de la otra rama y lo deja preparado, sin crear el commit. No conecta ambos historiales mediante un merge. | No lo usamos en los ejercicios 3 y 4. |
| **Squash Merge and commit** | Combina el resultado y crea un solo commit si no hay conflictos; de haberlos, debes resolverlos antes de terminar. | No lo usamos en los ejercicios 3 y 4. |
| **Cancel** | Cierra el menú sin iniciar la integración. | Para salir si seleccionaste una rama equivocada. |

Los textos pueden variar ligeramente entre versiones. Elige la opción por su nombre completo: `M` abre un menú, no completa el merge por sí sola. El squash del ejercicio 7 ocurre en **Commits**, con `s`; no es este menú de integración de ramas.

## Cómo completar los diálogos

- **Crear rama:** selecciona primero la rama de origen en Branches, pulsa `n`, escribe el nombre completo y pulsa `Enter`. Si se pregunta si quieres cambiar a ella, elige **Checkout / Yes**. Comprueba el nombre de la rama activa antes de editar.
- **Crear commit:** en Files, prepara solo los archivos indicados con `Espacio`, pulsa `c`, escribe el mensaje en **Summary** y pulsa `Enter` para confirmar. Si tu formulario usa otro atajo, lo muestra en el pie. Un commit guarda solo lo preparado.
- **Confirmar rebase, squash o cherry-pick:** revisa los nombres y el sentido de la acción; selecciona **Confirm / Yes** y pulsa `Enter`. **Cancel / Esc** cierra sin aceptarla.
- **Continuar una operación:** `m` minúscula abre las opciones de la operación en curso. **Continue** intenta terminar después de resolver y preparar los archivos; **Abort** cancela y vuelve al estado anterior. No elijas **Skip**: omitiría un commit.
- **Editor externo:** si Git abre un editor para un mensaje, guarda y cierra para continuar. En Vim: `Esc`, escribe `:wq` y pulsa `Enter`. En Nano: `Ctrl+O`, `Enter`, `Ctrl+X`.

## 1. Tu primer commit: editar, revisar y guardar

1. En **Branches**, selecciona `main` y pulsa `Espacio`. Con `main` seleccionada, pulsa `n`, escribe `practica/01-commits` y confirma. Verifica que esta sea la rama activa.
2. En tu editor abre `cafeteria/menu.txt`. Agrega `Chocolate: 1700` y guarda.
3. Vuelve a Lazygit. En **Files**, selecciona el archivo: a la derecha verás la línea agregada. Pulsa `Espacio` para prepararlo.
4. Pulsa `c`, escribe `feat: agregar chocolate al menu` y confirma el formulario siguiendo su pie de ayuda.
5. En **Commits**, selecciona el nuevo commit y pulsa `Enter` para revisar su archivo y su diff.

**Comprueba:** Files queda vacío y el nuevo mensaje aparece arriba de Commits. Cambia a `main`: el chocolate desaparece del archivo. Regresa a `practica/01-commits`: vuelve a aparecer. Cambiar de rama actualiza los archivos a esa versión.

**Lo que acabas de hacer:**

```text
main:                 A
                       \
practica/01-commits:     B  (+ chocolate)
```
A es la base; B es tu primer commit. `main` sigue en A.

## 2. Dos cambios, dos commits

1. Continúa en `practica/01-commits`. Agrega `Té frío: 1400` a `cafeteria/menu.txt` y una nueva tarea a `cafeteria/tareas.md`.
2. En **Files**, prepara únicamente `menu.txt` con `Espacio`. Pulsa `c` y guarda el mensaje `feat: agregar te frio`.
3. Observa que `tareas.md` sigue pendiente. Prepáralo y crea `docs: actualizar tareas`.

**Comprueba:** hay dos commits nuevos, cada uno con un solo archivo. Staging permite decidir qué cambios viajan juntos.

**Lo que acabas de hacer:**

```text
A ── B ── C ── D  ← practica/01-commits
     │    │    └─ solo tareas.md
     │    └────── solo menu.txt: té frío
     └─────────── menu.txt: chocolate
```
Cada commit tiene una intención. El archivo que no preparaste quedó pendiente hasta el siguiente commit.

## 3. Integrar una rama sin conflicto

1. En **Branches**, cambia a `main`. Selecciona `main`, pulsa `n` y crea `practica/03-merge`.
2. Sin cambiar la rama activa, mueve el cursor a `escenario/promocion`.
3. Pulsa `M`, elige **Regular Merge (fast-forward)** con las flechas y pulsa `Enter`. Si se solicita confirmación, acepta **Confirm / Yes**. El destino debe ser `practica/03-merge`. No elijas squash.
4. Abre `cafeteria/promociones.txt` y revisa el historial.

**Comprueba:** aparece la promoción. Con la opción indicada ocurre un **fast-forward**: Git solo adelanta el puntero de tu rama porque no hay historias divergentes; no necesita un commit de merge nuevo. `main` conserva su posición.

**Lo que acabas de hacer:**

```text
Antes:   A  ← practica/03-merge
          \
           P  ← escenario/promocion

Después: A ── P  ← practica/03-merge, escenario/promocion
         ↑
        main
```
El puntero de tu práctica avanzó hasta P; no se creó un commit adicional.

## 4. Resolver un conflicto de verdad

Dos personas cambiaron el precio del mismo café desde la misma base.

1. En **Branches**, selecciona `escenario/precio-local`, pulsa `n` y crea `practica/04-conflicto`. Verifica que estás en esta nueva rama.
2. Selecciona `escenario/precio-equipo` sin cambiarte a ella. Pulsa `M`, selecciona **Regular Merge** (sin la variante fast-forward) y pulsa `Enter`. Si aparece otro diálogo, acepta **Confirm / Yes**. El destino debe ser `practica/04-conflicto`; no elijas ninguna opción Squash.
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
6. Vuelve a **Files** y prepara `menu.txt` con `Espacio`. Pulsa `m` para abrir las opciones de merge/rebase y elige **Continue** y pulsa `Enter`. Si se solicita mensaje, conserva el propuesto, guarda y cierra el editor. Si Lazygit ya terminó el merge al preparar el último archivo, verifica el nuevo commit y no inicies otra operación.

**Comprueba:** no quedan archivos en conflicto; el café cuesta 1700 y el commit de merge tiene dos padres. Puedes ver el grafo con `git log --graph --oneline --all` en otra terminal.

Si quieres cancelar el intento mientras está en curso, pulsa `m` y selecciona **Abort merge**; volverás al estado anterior a la integración. Hazlo antes de empezar otra práctica.

**Lo que acabas de hacer:**

```text
          L (1600) ── M (1700)  ← practica/04-conflicto
         /          /
A ──────┤          /
         \        /
          E (1800)             ← escenario/precio-equipo
```
M une L y E. Elegiste manualmente el contenido final: 1700. Las ramas de escenario conservan sus precios originales.

## 5. Guardar una interrupción con stash

1. Cambia a `main` y crea `practica/05-stash` con `n`.
2. Agrega `Revisar inventario` a `cafeteria/tareas.md`, guarda, pero no hagas commit.
3. En **Files**, pulsa `s` y escribe una descripción si se solicita. Esto guarda temporalmente tus cambios.
4. Comprueba que Files queda vacío. Cambia a `main` y después regresa a `practica/05-stash`.
5. En el panel **Stash**, selecciona tu entrada, pulsa `g` (**Apply**, compruébalo con `?` si tu configuración difiere) y acepta **Confirm / Yes** si aparece un diálogo. Apply recupera los cambios y conserva la entrada; Pop los recupera y la elimina si tiene éxito.
6. Revisa Files, prepara el archivo y crea `docs: revisar inventario`. Después, en Stash, selecciona esa misma entrada, pulsa `d` (**Drop**), revisa la descripción y confirma su eliminación. Ya tienes el cambio guardado en el commit.

**Comprueba:** recuperaste la tarea y la guardaste en un commit. Un stash no se recupera automáticamente al regresar a una rama.

**Lo que acabas de hacer:**

```text
Archivo editado ── stash ──► guardado temporal
                                │ Apply
                                ▼
Archivo recuperado ── staging ── commit
```
Apply conserva la entrada del stash; por eso la eliminaste después de guardar el commit.

## 6. Rebase: colocar tu trabajo sobre una base nueva

1. En **Branches**, selecciona `escenario/rebase-feature`, pulsa `n` y crea `practica/06-rebase`.
2. En **Commits**, observa los dos commits `feat: agregar horario...` y `docs: ampliar horario...`. Opcionalmente anota sus identificadores.
3. En **Branches**, selecciona `escenario/rebase-base` sin cambiarte a ella. Pulsa `r`; el diálogo debe indicar que rebasarás `practica/06-rebase` sobre `escenario/rebase-base`. Selecciona **Confirm / Yes** y pulsa `Enter`. Si los nombres están al revés, cancela con `Esc` y comprueba la rama activa.
4. Revisa el historial y los archivos `cafeteria/horarios.txt` y `cafeteria/contacto.txt`.

**Comprueba:** tus dos commits están ahora encima de `chore: agregar contacto de cafeteria`; sus identificadores cambiaron y los archivos de ambas ramas están presentes. Rebase vuelve a crear tus commits sobre otra base. Aquí trabajas con copias locales propias.

**Lo que acabas de hacer:**

```text
Antes:       A ── H1 ── H2  ← tu práctica
              \
               C           ← escenario/rebase-base

Después:     A ── C ── H1' ── H2'  ← practica/06-rebase
```
C agrega contacto; H1 y H2 agregan horarios. Las comillas indican versiones nuevas de esos commits, con identificadores nuevos.

## 7. Limpiar dos commits con squash

1. Selecciona `escenario/rebase-feature` y crea `practica/07-squash` con `n`.
2. En **Commits**, selecciona el más reciente: `docs: ampliar horario de fin de semana`.
3. Pulsa `s` para unirlo con el commit inmediatamente anterior, `feat: agregar horario de cafeteria`. Selecciona **Confirm / Yes** en el diálogo de squash y pulsa `Enter`; si aparece un editor de mensaje, escribe `feat: definir horarios de cafeteria`, guarda y cierra.
4. Si necesitas ajustar el mensaje después, selecciona el commit resultante y usa `r`.

**Comprueba:** los dos commits del horario se convirtieron en uno y `cafeteria/horarios.txt` conserva las dos líneas. Squash cambia el historial, no el contenido final.

**Lo que acabas de hacer:**

```text
Antes:    A ── H1 ── H2  ← practica/07-squash
Después:  A ── H        ← practica/07-squash
```
H contiene los cambios de H1 y H2 juntos. El archivo final conserva ambos horarios.

## 8. Traer solo un commit con cherry-pick

1. Cambia a `escenario/promocion`. En **Commits**, selecciona `feat: agregar promocion de desayuno` y pulsa `C` (Mayús+c) para marcarlo.
2. En **Branches**, cambia a `main`, selecciona `main` y crea `practica/08-cherry-pick` con `n`.
3. En **Commits**, pulsa `V` (Mayús+v) para aplicar el commit marcado. En la confirmación de cherry-pick, selecciona **Confirm / Yes** y pulsa `Enter`. No cambies de rama después de pegarlo.

**Comprueba:** tu rama contiene la promoción sin integrar otras ramas enteras. Cherry-pick aplica el cambio de un commit en la rama activa; su identificador puede ser diferente.

**Lo que acabas de hacer:**

```text
Origen:   A ── P   ← escenario/promocion
               ⋮ copiar el cambio (C), pegarlo (V)
Destino:  A ── P*  ← practica/08-cherry-pick
```
P* aplica el mismo cambio en el destino; no es un commit de merge. En este ejemplo mínimo Git puede generar el mismo identificador si coinciden también padre y metadatos.

## Reiniciar todo con `restart`

Cierra Lazygit con `q`. En la terminal, desde la carpeta del repositorio:

```sh
./restart --dry-run  # Muestra qué se restaurará, sin modificar nada.
./restart            # Escribe RESTART cuando se solicite.
lazygit              # Comienza otra vez desde el ejercicio 1.
```

Para un reinicio sin pregunta, usa `./restart --yes`. Requiere Python 3 y Git.

**Reiniciar elimina el progreso de este repositorio:** descarta ediciones preparadas y pendientes, borra archivos no versionados e ignorados (incluidas carpetas), vacía los stashes y elimina las ramas y etiquetas adicionales. Restaura `main` y las cinco ramas de escenario desde `inicio/...`, conservando esta guía y el script. También aborta merges, rebases y cherry-picks pendientes. No modifica repositorios remotos ni carpetas externas. No guardes aquí archivos que quieras conservar antes de ejecutarlo.

Los commits de práctica dejan de estar en las ramas y etiquetas del laboratorio. Git puede conservarlos temporalmente en el reflog: esto restaura el ejercicio, no realiza un borrado forense de objetos. El script rechaza repositorios con varios worktrees para no alterar otro directorio de trabajo. Conserva las etiquetas `inicio/...`: son la base del reinicio.

No he ejecutado el reinicio sobre tu práctica terminada; tú decides cuándo hacerlo.

```text
Ramas de práctica + cambios + stash
                 │ ./restart
                 ▼
main + escenarios originales + guía + script
                 │
                 └─ listo para repetir los 8 ejercicios
```

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
