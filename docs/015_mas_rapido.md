# MUDARSE AÚN MÁS RÁPIDO CON VIM SURROUND e EASYMOTION

[Vim-sneak](https://github.com/justinmk/vim-sneak) y [vim-EasyMotion](https://github.com/easymotion/vim-easymotion) son un par de complementos de Vim que aumentan la velocidad con la que puede moverse en Vim.

Ambos complementos deben habilitarse a través de la configuración de VSCodeVim. Para habilitarlos, solo vaya a *Preferencias* , Búsqueda de *configuraciones* para *vim sneak* o *vim easymotion* y encontrará el interruptor.

## VIM-FURTIVAMENTE

**Vim-sneak es un término medio entre la búsqueda de caracteres (dentro de una línea) y la búsqueda de patrones (dentro de un archivo)** :

- Escriba **`s{char}{char}`**y el cursor vuela a la primera aparición de esa secuencia de dos caracteres.
- A partir de entonces, escriba **`;`**para la próxima aparición o **`,`**para la anterior.
- **`S{char}{char}`** funciona de manera similar pero al revés.

Donde *vim-surround* extendió el lenguaje secreto de Vim con un operador, *vim-sneak* hace lo mismo pero con un movimiento: **el movimiento furtivo** . Como tal, puede usarlo en combinación con otros operadores:

- Escriba **`{operator}z{char}{char}`**y el operador se aplicará sobre el texto atravesado por el movimiento furtivo.

### ¿POR QUÉ Z EN LUGAR DE S?

Cuando se usa junto con otros operadores, vim-sneak usa el `z`porque `s`ya está tomado por vim-surround. Y vim-surround es un complemento Vim extremadamente popular.

## VIM-EASYMOTION

**Vim-EasyMotion** intenta simplificar el uso de movimientos en Vim eliminando la necesidad de contar. En lugar de mirar un fragmento de código, contar en tu cabeza y usar cualquiera de estas combinaciones para realizar alguna acción:

```text
{operator}{count}{motion}
```

o moverse:

```text
{count}{motion}
```

cuando activa un movimiento con EasyMotion, etiqueta los posibles objetivos en todo el documento con una combinación de teclas que se muestra en una superposición (sobre el texto en cuestión). Escriba esa combinación de teclas y se teletransportará a esa ubicación de inmediato.

Por ejemplo, type **`w`**y EasyMotion etiquetarán el comienzo de todas las palabras delante de usted de la siguiente manera:

![Pasar al comienzo de las palabras en movimiento fácil](https://www.barbarianmeetscoding.com/images/vscodevim-easymotion.jpg)

*¡Esto es lo que sucede cuando disparas un movimiento con EasyMotion! : O*

En el ejemplo de la imagen, escribir la letra **`l`**haría que el cursor saltara a la `FactionShipModifiers`interfaz, mientras que escribir **`p`**te enviaría a la `Energy`propiedad de esa interfaz.

O puede escribir **`f'`**y EasyMotion etiquetará todas las apariciones del **`'`**personaje en las líneas actuales y posteriores. Bastante ingenioso, ¿no?

Todos los movimientos proporcionados por vim-EasyMotion tienen espacios de nombres **``**y utilizan enlaces de teclas cuyo significado está relacionado con los movimientos principales de Vim:

| mando         | mover a…                                                     |
| :------------ | :----------------------------------------------------------- |
| **`w`**       | comienzo de palabras                                         |
| **`b`**       | comienzo de palabras al revés                                |
| **`bdw`**     | comienzo de palabras en todas partes. Los **`bd`**stands para bidireccional |
| **`e`**       | fin de las palabras                                          |
| **`ge`**      | fin de las palabras al revés                                 |
| **`bdw`**     | fin de las palabras en todas partes                          |
| **`j`**       | comienzo de líneas                                           |
| **`k`**       | comienzo de líneas hacia atrás                               |
| **`f{char}`** | encontrar personaje                                          |
| **`F{char}`** | encontrar el personaje al revés                              |
| **`t{char}`** | hasta el personaje                                           |
| **`T{char}`** | hasta que el personaje retroceda                             |
| **`s{char}`** | buscar personaje en todas partes                             |

### EASYMOTION SOLO FUNCIONA PARA MOVERSE

En la versión VSCodeVim, los movimientos en EasyMotion solo admiten moverse y no se pueden combinar con operadores. Esta es una característica que es compatible con Vim tradicional, por lo que puede ser algo que vendrá a VSCodeVim en el futuro.