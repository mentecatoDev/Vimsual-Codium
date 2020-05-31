# EDICIÓN REUTILIZABLE CON MACROS

### ¡EL SOPORTE PARA MACROS EN VSCODEVIM ES LIMITADO!

El soporte para macros en VSCodeVim no es tan bueno como en Vim, pero decidí incluirlo porque puede ser útil en algunas situaciones como pronto verá. Algunas características más avanzadas de las macros, como editar macros existentes o guardar macros como asignaciones personalizadas, son imposibles o muy inconvenientes en VSCodeVim.

A Vim le encanta ahorrar tiempo y molestias, y le ofrece muchas formas de repetir comandos:

- El **`.`**comando le permite repetir el último cambio.
- El **`;`**y **`,`**comandos le permiten repetir la última búsqueda de caracteres delante y hacia atrás, respectivamente.
- **`n`**y le **`N`**permite repetir la última búsqueda también hacia adelante y hacia atrás.
- **`/`**y **`?`**también le permite repetir la última búsqueda hacia adelante o hacia atrás.
- **`:@`**y **`@@`**te permite repetir comandos Ex.

**Las macros de Vim llevan este poder de repetición al siguiente nivel al permitirle grabar una colección de comandos a medida que los escribe y luego reproducirlos a voluntad** . Como tal, las macros se convierten en acciones de edición reutilizables que pueden ahorrarle mucho tiempo.

## CREAR UNA NUEVA MACRO DE VIM

Crea una nueva macro siguiendo este proceso:

1. Escriba **`q{register}`**para comenzar a grabar una macro (por ejemplo **`qq`**, comenzará a grabar una macro para registrar **`q`**) dentro de un registro.
2. Realice las diferentes acciones que desea incluir en la macro.
3. Cuando haya terminado, escriba **`q`**para finalizar la grabación.

A partir de ese momento, puede reproducir la macro cuando lo desee:

- Escriba **`@{register}`**(por ejemplo **`@q`**) para ejecutar la macro que vive en un determinado **`register`**.

Una vez que haya ejecutado una macro una vez, puede repetir la última macro escribiendo **`@@`**. Esto sigue el mismo espíritu de los otros comandos repetidores en Vim.

## MACROS EN ACCIÓN

Usemos un ejemplo para ilustrar el uso de macros en Vim. Imagina que tienes una lista de algunos artículos comunes que puedes encontrar en cualquier tienda de juegos de rol de fantasía de 8 bits vendida por un NPC extremadamente aburrido. Están separados por comas como esta:

```text
rusty sword,obsidian dagger,silver poniard,broadsword
```

Y ahora imagina que quieres tomar esa lista y convertirla en HTML. *Web 1.0 aquí vamos* . El HTML resultante se vería así:

```html
<ul>
  <li>rusty sword</li>
  <li>obsidian sword</li>
  <li>silver poniard</li>
  <li>broadsword poniard</li>
</ul>
```

Un posible enfoque para resolver este problema es crear una macro que encapsule el proceso de tomar un elemento de una lista y ponerlo dentro de un `li`elemento.

Entonces, comenzando con el cursor en la primera letra de la lista:

```text
v
rusty sword,obsidian dagger,silver poniard,broadsword
```

podemos hacer lo siguiente:

1. Comience por grabar la macro en el **`q`**registro con **`qq`**.
2. Luego usa **`f,`**para encontrar el primero **`,`**.
3. Escriba **`cwk`**para eliminar la coma y mover la lista, pero para el primer elemento a la siguiente línea, luego haga una copia de seguridad:

```text
   --- cursor is here
  /
 /
|
v
rusty sword
obsidian dagger,silver poniard,broadsword
```

1. Ahora **`I`**para insertar la etiqueta de apertura.
2. Luego **`A`**para insertar la etiqueta de cierre.
3. Moverse al comienzo de la línea de abajo **`j0`**.
4. Termine de grabar la macro escribiendo **`q`**:

```text
<li>rusty sword</li>
obsidian dagger,silver poniard,broadsword
^
 \
  \
   ----- cursor is here
```

Ahora solo escribe `@q`para reproducir la macro y obtendrás esto:

```text
<li>rusty sword</li>
<li>obsidian dagger</li>
silver poniard,broadsword
```

Ahora escriba `@@`para repetir la última macro:

```text
<li>rusty sword</li>
<li>obsidian dagger</li>
<li>silver poniard</li>
broadsword
```

Si intenta usar nuestra macro nuevamente, se sorprenderá al descubrir que no sucede nada. ¿Por qué? Como Vim no puede encontrar ninguna coma, la macro deja de ejecutarse. Podemos solucionar esto agregando una coma al final antes de comenzar a procesar la línea de elementos:

```text
rusty sword,obsidian dagger,silver poniard,broadsword,
```

Y ahora, si combinamos el poder de los contadores con las macros, podemos procesar toda la línea de elementos a la vez. Tipo `4@q`:

```html
<li>rusty sword</li>
<li>obsidian dagger</li>
<li>silver poniard</li>
<li>broadsword</li>
```

Has completado tu tarea ( **baile de la victoria** ).

Espero que este ejemplo sea ilustrativo del poder de las macros y sirva de inspiración en futuras sesiones de codificación. **Lo mejor de las macros es que puede usar las mismas técnicas (movimientos, operadores, recuentos, etc.) que normalmente usa para escribir código y empaquetarlas para que puedan reutilizarse más tarde** .

### EDICIÓN Y GUARDADO DE MACROS

Editar y guardar macros como asignaciones personalizadas son características potentes, pero hasta que no se admitan correctamente en VSCodeVim no tiene sentido escribir sobre ellas. Sería confuso. Pero no se preocupe, si estas características llegan a VSCodeVim, actualizaré el libro para reflejarlo.