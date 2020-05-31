# Ampliando los límites de copiar y pegar

**Copia y pega**. No es muy emocionante, ¿verdad?. Probablemente estés acostumbrado a usar tu ratón para seleccionar texto, copiarlo o cortarlo, y luego pegarlo en otro lugar. Eso es todo. No hay mucho con qué emocionarse.

Vim hace que copiar, cortar un poco sea más interesante:

- Cuenta con operadores brillantes y comandos que puedes usar en combinación con todos los movimientos que has aprendido hasta ahora
- Proporciona un puñado de registros donde puedes guardar cosas para más adelante, lo que puede permitir flujos de trabajo interesantes y ayudarte a recuperar texto cuando lo eliminas por error

Los dos principales para copiar y pegar son **`y`** y **`p`**. *¿Por qué se usa **`y`** en lugar de **`c`** **c**opy?*. Bueno, si recuerdas de los capítulos anteriores **`c`** ya está en uso, es el comando **cambiar** (*change*). Por lo tanto, los ingenieros de **Vi** tuvieron que dar con una manera colorida para describir copiar y se les ocurrió **y**ank (*tirar*). Así que, en Vim no copias cosas, sino **tiras** de ellas (excelente nombre... ¡qué visceral!). **`p`** significa **p**ut pero podemos ignorar eso por seguridad y seguir llamándolo ***p**aste*. Porque somos rebeldes e indomables, y no nos importa lo que el mundo pueda pensar de nosotros.

![Vim copiar y pegar comandos](https://www.barbarianmeetscoding.com/images/vim-copy-paste-commands.jpg)

### Yanking

**`y`** es un operador. Puedes combinarlo con cualquiera de los movimientos y objetos de texto que hayas aprendido para tirar de cosas según desee tu corazón:

- **`yl`** **y**anks una **l**etra
- **`yaw`** **y**anks una **w**ord,
- **`yas`** **y**anks una **s**entencia
- **`yi(`** **y**anks todo dentro de los **`(`**, y así sucesivamente...

Si se duplica **`y`** como en **`yy`** obtenemos **un operador sobre líneas completas**, como con **`dd`** y **`cc`**, es decir, un "tirón" a una línea entera. El **`Y`** comando también tira de una línea completa. Prefiero usar, **`yy`** pero no dudes en elegir el que quieras.

### Pegado

Para pegar cosas, usa el comando **`p`** y sus variantes:

- **`p`** pega algo después del cursor
- **`P`** pega algo antes del cursor
- **`gp`** igual que **`p`** pero coloca el cursor después de la selección pegada
- **`gP`** igual que **`P`** y coloca el cursor después de la selección pegada

¡Esto es una flexibilidad asombrosa para pegar!

Pegar en Vim es algo especial y el comportamiento de **`p`** y **`P`** depende de si has partido de caracteres o líneas. Si se han copiado **caracteres**, al pegarlos se colocarán después o antes del cursor (no hay sorpresas allí). Sin embargo, si se han copiado **líneas**, al pegar se colocarán antes o después de la línea sobre la que descansa el cursor.

![Vim útil pegar copia](https://www.barbarianmeetscoding.com/images/vim-useful-copy-pasting.jpg)

**¿Quieres duplicar una línea?**. Es tan fácil como escribir **`yyp`**. *¿Quieres n-plicar una línea?*. Es tan simple como escribir **`yy{count}p`**. ¡Si!. ¡Las cuentas también funcionan con tirar y pegar porque son solo comandos! (lo siento... me emocioné demasiado).

Si **`y`** copia cosas... ¿Cómo se cortan cosas en Vim? **¡Ajá! ¡Aquí viene una sorpresa!**.

## Cortar cosas en Vim

*¿Recuerdas `d` y `c` de hace 10 minutos?*. Bueno, cuando dije que borraste el texto en el olvido, **¡mentí!**. En realidad se **cortan** cosas. Estabas cortando texto todo el tiempo y ni siquiera te diste cuenta. Texto que luego puedes pegar si eso es lo que quieres (**mindblown**).

**¿Quieres intercambiar algunos caracteres?**. Escribe **`dlp`** (o **`xp`**). *¿Quieres intercambiar un par de líneas?*. Escribe **`ddp`**.

¡Excelente! Así que ahora has aumentado tu conocimiento con tirones, cortes y pegados en Vim. Pero aún queda un elemento que aún no hemos tocado: los **registros**.

## Copiado múltiple y corte con registros

Los registros son como un portapapeles especial donde puedes guardar varias cosas a la vez. Los siguientes registros son súper útiles:

- El **registro sin nombre** **`"`** es donde se copian y cortan cosas, cuando no especificas explícitamente un registro. Vamos, el registro predeterminado si lo deseas ver de ese modo.
- Los **registros con nombre** **`a-z`** son registros que puedes usar explícitamente para copiar y cortar texto a voluntad.
- El **registro de extracción** **`0`** almacena lo último que has (copiado).
- Los **registros de corte** **`1-9`** almacenan las últimas 9 cosas que se cortaron utilizando el comando eliminar o cambiar.

Los **registros con nombre te** permiten guardar fragmentos de textos para pegarlos más tarde. Puedes guardar explícitamente en un registro utilizando el siguiente comando:

```text
"{nombre del registro}y{motion}
"{nombre del registro}d{motion}
"{nombre del registro}c{motion}
```

Por ejemplo, **`"ayas`** tira de una oración y la almacena en el registro **`a`**. Ahora, si deseas pegarlo en otro lugar, puedes escribir **`"ap`**. Alternativamente, si usas la versión en mayúsculas de un registro (es decir,**`A`** en lugar de **`a`**) agregas lo que copies o cortes en ese registro.

El **registro de** extracción te permite tener acceso a lo que copiaste por última vez a través del comando **`y`**. Esto es útil porque las eliminaciones y los cambios no sobrescriben este registro como sí lo hacen con el registro sin nombre.

Los **registros de corte te** dan acceso a las últimas 9 cosas que eliminaste o modificaste. Esto es genial si hay algún texto que eliminaste anteriormente y que deseas recuperar.

En cualquier momento, puedes usar el comando `:reg` para ver qué hay en tus registros. O puedes escribir `:reg {register}` para inspeccionar el contenido de un registro específico.

## Pegar en modo insertar

Todos los comandos que hemos visto hasta ahora funcionan en *modo Normal* . ¿Qué pasa si quieres pegar algo cuando estás en *modo Insertar* ? Bueno, puedes hacer eso también. Utilizando `CTRL-R {register}` puedes pegar el contenido de un registro después del cursor:

- **`CTRL-R "`** pega el contenido del registro sin nombre
- **`CTRL-R a`** pega el contenido del registro **`a`**
- **`CTRL-R 0`** pega el contenido del registro de extracción

Al ser Visual Studio Code, significa que también puedes confiar en que tu sistema copie y pegue claves para pegar texto en el **modo Insertar**. Probablemente sea lo más conveniente para tí en la mayoría de los casos.

Un consejo final. El uso del *modo Insertar* para pegar desde un registro elimina la limitación de la extracción y el pegado de líneas. Entonces, utilizando este método, puedes tirar de una línea y luego pegarla justo después del cursor. ¡Ahora ve y disfruta de copiar y pegar de verdad!.