# Cursores múltiples

Si eres un usuario incondicional de Visual Studio Code, es probable que uses varios cursores. VSCodeVim ofrece un soporte experimental para múltiples cursores en modos *Visual* y *Normal*. Con esta función experimental (que está habilitada de manera predeterminada), puedes generar múltiples cursores y luego usar operadores para liberar el poder de Vim en múltiples ubicaciones a la vez. **¡GUAUU!**

## Agregar múltiples cursores basados en la búsqueda por palabras

Si deseas **agregar múltiples cursores basados en la búsqueda por palabras** debes:

1. Mover el cursor sobre una palabra de tu código.
2. Escribir **`CTRL-D`** o **`gb`** para agregar otro cursor. Esto pone a Vim en *modo Visual* y listo para operar en la palabra que has seleccionado.
3. Escribe **`CTRL-D`** o **`gb`** continúa agregando cursores hasta que hayas terminado.
4. Ahora puedes realizar una acción en *modo Visual* (eliminar, cambiar, etc.) o,
5. Regresar al *modo Normal* con **`<ESC>`** y escribir cualquier comando del *modo Normal* manteniendo los múltiples cursores.

Un posible caso de uso para múltiples cursores sería renombrar algo. Imagina que tienes una función que cambia el nombre de cosas, como las propiedades dentro de los objetos en JavaScript. Digamos que tienes este hermoso objeto que **me** representa a **mí**:

```javascript
const paco= {
  name: 'Paco',
  attributes: ['handsome', 'smart', 'witty']
};
```

Y algún día te cansas de toda esta auto adoración y narcisismo y quieres vengarte. Entonces decides cambiar el nombre de mi propiedad `attributes` a `lackingAttributes`:

```javascript
rename(paco, 'attributes', 'lackingAttributes');
```

Tal función (que ahora debes prometer que nunca escribirás en ningún programa) podría verse así:

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

La propiedad `name` no es lo suficientemente descriptiva, por lo que queremos cambiarle el nombre a `oldName` porque este ejemplo no podría tener otra meta que esta. Podemos lograr este cambio de nombre usando múltiples cursores:


1. Mueve el cursor hacia arriba `name` con el operador de búsqueda `/name<Enter>`,
2. Escribe **`gb`** tres veces para crear tres cursores en la parte superior de cada `name` variable,
3. Ahora estás en *modo Visual* con tres selecciones separadas,
4. Escribe `coldName<ESC>` para cambiar cada aparición de `name` por `oldName`.
5. Todavía tienes tres cursores y ahora estás en *modo Normal*. Puedes continuar jugando o eliminar todos los cursores adicionales escribiendo **`<ESC>`** una vez más.

Como alternativa, podrías haber escrito **`<ESC>`** en el paso **`4`** y luego usar el siguiente comando en *modo Normal*: **`ciwoldName<ESC>`**. La diferencia es que el *modo Visual* opera en la selección de texto actual (las palabras) y el *modo Normal te* permite operar en cualquier selección de texto utilizando movimientos arbitrarios basados en la posición de los cursores múltiples.

## Agregar múltiples cursores en líneas consecutivas

Si deseas **extender tus cursores hacia arriba o hacia abajo en líneas consecutivas**, entonces el mejor enfoque es confiar en el *modo de bloque visual*:

1. Escribe **`<CTRL-V>`** para saltar al modo *Visual-block*.
2. Usa **`j`**, **`k`** para seleccionar un rectángulo de texto hacia abajo o hacia arriba respectivamente.
3. Escribe **`I`** para insertar o **`A`** para agregar, luego escribe un texto y presiona **`<ESC>`**.
4. Alternativamente, usa cualquier comando del *modo Normal* para operar en el texto seleccionado de cada línea.

¿En qué puede serme útil esto, te preguntarás? Imagina una lista de las cosas que necesitarías para sobrevivir a un apocalipsis zombie:

```text
towel
wrench
shotgun
axe
rusty broadsword
sausage
chain-saw
```

Y ahora, debido a que dos cabezas son mejores que una, y que es posible que te hayas olvidado de algo importante, debes poner esa lista en un sitio web para compartirla con otros futuros supervivientes del apocalipsis zombie. Sitio web significa HTML, significa elementos HTML semánticos, significa que necesitamos ajustar esos elementos en el formato correcto. Cada objeto valioso estará envuelto en un *elemento* `<li>` (*elemento de lista*), y todos irán dentro de una `<ol>` (lista ordenada) porque el **orden es importante** y, cuando las cosas se ponen feas, prefiero tener una toalla en lugar de una motosierra. 

Entonces, suponiendo que el cursor esté en la parte superior de la primera letra de esa lista:

```text
v
towel
```

Escribirías:

1. **`CTRL-V`** para entrar en modo *Visual-block* ,
2. luego **`j`** hacia abajo hasta el final de la lista,
3. seguido de **`I`** para entrar en *modo Insertar* al comienzo del bloque,
4. y finalmente **`<li>`** y **`<ESC>`** para salir del *modo Insertar*

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

1. **`CTRL-V`** para entrar en modo *Visual-block*,
2. luego **`j`** hacia abajo hasta el final de la lista,
3. ahora usa el **`$`** movimiento para mover todos los cursores al final de cada línea,
4. escribe **`A`** para entrar en *modo Insertar* al final del bloque,
5. y finalmente **`</li>`** y **`<ESC>`**

```html
<li>towel</li>
<li>wrench</li>
<li>shotgun</li>
<li>axe</li>
<li>rusty broadsword</li>
<li>sausage</li>
<li>chain-saw</li>
```
