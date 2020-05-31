# CURSORES MÚLTIPLES

Si eres un usuario incondicional de Visual Studio Code, es probable que uses varios cursores. VSCodeVim ofrece un soporte experimental para múltiples cursores en modos *Visual* y *Normal* . Con esta función experimental (que está habilitada de manera predeterminada), puede generar múltiples cursores y luego usar operadores para liberar el poder de Vim en múltiples ubicaciones a la vez. **¡GUAUU!**

## AGREGAR MÚLTIPLES CURSORES BASADOS EN LA BÚSQUEDA DE PALABRAS

Si desea **agregar múltiples cursores basados en la búsqueda de palabras** , debe:

1. Mueva el cursor sobre una palabra en su código.
2. Escriba **``**( **`CTRL-D`**en Windows / Linux) o **`gb`**para agregar otro cursor. Esto pone a Vim en *modo Visual* y listo para operar en la palabra que ha seleccionado.
3. Escriba **``**( **`CTRL-D`**en Windows / Linux) o **`gb`**continúe agregando cursores hasta que haya terminado.
4. Ahora puede realizar una acción en *modo Visual* (eliminar, cambiar, etc.) o,
5. Regrese al *modo Normal* con **``**y escriba cualquier comando del *modo Normal* manteniendo los múltiples cursores.

Un posible caso de uso para múltiples cursores sería renombrar algo. Imagine que tiene una función que cambia el nombre de cosas, como las propiedades dentro de los objetos en JavaScript. Digamos que tienes este hermoso objeto que **me** representa a **mí** :

```javascript
const jaime = {
  name: 'Jaime',
  attributes: ['handsome', 'smart', 'witty']
};
```

Y algún día te cansas de toda esta auto adoración y narcisismo y quieres vengarte. Entonces decide cambiar el nombre de mi propiedad `attributes`a `lackingAttributes`:

```javascript
rename(jaime, 'attributes', 'lackingAttributes');
```

Tal función (que ahora debe prometer nunca escribir en ningún programa) podría verse así:

```text
function rename(obj, name, newName){
  Object.defineProperty(obj, newName, { 
                  value: obj[name], 
                  enumerable: true,
                  writable: true,
                  configurable: true
  });
  delete obj[name];
}
```

La `name`propiedad no es lo suficientemente descriptiva, por lo que queremos cambiarle el nombre `oldName`porque este ejemplo no podría ser más meta que esto. Podemos lograr este cambio de nombre usando múltiples cursores:

1. Mueve el cursor hacia arriba `name`con el operador de búsqueda `/name`,
2. Escriba **`gb`**tres veces para crear tres cursores en la parte superior de cada `name`variable,
3. Ahora estás en *modo Visual* con tres selecciones separadas,
4. Escriba `coldName`para cambiar cada aparición de `name`for `oldName`.
5. Todavía tiene tres cursores y ahora está en *modo Normal* . Puede continuar jugando o eliminar todos los cursores adicionales escribiendo **``**una vez más.

Como alternativa, podría haber escrito **``**en el paso **`4`**y luego se usa el siguiente *modo Normal* comando: **`ciwoldName`**. La diferencia es que el *modo Visual* opera en la selección de texto actual (las palabras) y el *modo Normal le* permite operar en cualquier selección de texto utilizando movimientos arbitrarios basados en la posición de los cursores múltiples.

## AGREGAR MÚLTIPLES CURSORES EN LÍNEAS CONSECUTIVAS

Si desea **extender sus cursores hacia arriba o hacia abajo en líneas consecutivas** , entonces el mejor enfoque es confiar en el *modo de bloque visual* :

1. Escriba **``**jupm en modo *Visual-block* .
2. Use **`j`**, **`k`**para seleccionar un rectángulo de texto hacia abajo o hacia arriba respectivamente.
3. Escriba **`I`**para insertar o **`A`**agregar, luego escriba un texto y presione **``**.
4. Alternativamente, use cualquier comando del *modo Normal* para operar en el texto seleccionado en cada línea.

¿Cómo puede ser útil, preguntas? Imagine una lista de las cosas que necesitaría para sobrevivir a un apocalipsis zombie:

```text
towel
wrench
shotgun
axe
rusty broadsword
sausage
chain-saw
```

Y ahora, debido a que dos cabezas son mejores que una, y es posible que hayas olvidado algo importante, debes poner esa lista en un sitio web para compartirla con otros futuros sobrevivientes del apocalipsis zombie. Sitio web significa HTML, significa elementos HTML semánticos, significa que necesitamos ajustar esos elementos en el formato correcto. Cada objeto valioso estará envuelto en un *elemento*`` ( *elemento de la lista* ), y todos irán dentro de una ``(lista ordenada) porque el **orden es importante** y, cuando se trata de empujar, prefiero tener una [toalla en lugar](https://www.barbarianmeetscoding.com/boost-your-coding-fu-with-vscode-and-vim/multiple-cursors/#fn-towel) de una cadena -Sierra.

Entonces, suponiendo que el cursor esté en la parte superior de la primera letra de esa lista:

```text
v
towel
```

Escribirías:

1. **`CTRL-V`**para entrar en modo *Visual-block* ,
2. luego **`j`**hacia abajo hasta el final de la lista,
3. seguido de **`I`**para entrar en *modo Insertar* al comienzo del bloque,
4. y finalmente **``**y **``**para salir del *modo Insertar*

Resultando en lo siguiente:

```html
<li>towel
<li>wrench
<li>shotgun
<li>axe
<li>rusty broadsword
<li>sausage
<li>chain-saw
```

Ahora repita el proceso para agregar la etiqueta de cierre:

1. **`CTRL-V`**para entrar en modo *Visual-block* ,
2. luego **`j`**hacia abajo hasta el final de la lista,
3. ahora usa el **`$`**movimiento para mover todos los cursores al final de cada línea,
4. escriba **`A`**para entrar en *modo Insertar* al final del bloque,
5. y finalmente **``**y**``**

```html
<li>towel</li>
<li>wrench</li>
<li>shotgun</li>
<li>axe</li>
<li>rusty broadsword</li>
<li>sausage</li>
<li>chain-saw</li>
```