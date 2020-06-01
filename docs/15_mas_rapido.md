# Mudarse aún más rápido con vim surround e easymotion

[Vim-sneak](https://github.com/justinmk/vim-sneak) y [vim-EasyMotion](https://github.com/easymotion/vim-easymotion) son un par de complementos de Vim que aumentan la velocidad con la que puedes moverte en Vim.

> Ambos complementos deben habilitarse a través de la configuración de VSCodeVim. Para habilitarlos, solo ve a *Preferences*, *Settings*, buscar *vim sneak* o *vim easymotion* y encontrarás el switch.

## Vim-sneak (furtivo)

**Vim-sneak es un término medio entre la búsqueda de caracteres (dentro de una línea) y la búsqueda de patrones (dentro de un archivo)**:

- Escribe **`s{char}{char}`** y el cursor vuela a la primera aparición de esa secuencia de dos caracteres.
- A partir de entonces, escriba **`;`** para la próxima aparición o **`,`** para la anterior.
- **`S{char}{char}`** funciona de manera similar pero al revés.

Donde *vim-surround* extendió el lenguaje secreto de Vim con un operador, *vim-sneak* hace lo mismo pero con un movimiento: **el movimiento furtivo**. Como tal, puedes usarlo en combinación con otros operadores:

- Escribe **`{operator}z{char}{char}`** y el operador se aplicará sobre el texto atravesado por el movimiento furtivo.

> ### ¿Por qué `z` en lugar de `s`?
>
> Cuando se usa junto con otros operadores, vim-sneak usa la `z` porque `s` ya está tomada por vim-surround. Y vim-surround es un complemento Vim extremadamente popular.

## Vim-EasyMotion

**Vim-EasyMotion** intenta simplificar el uso de movimientos en Vim eliminando la necesidad de contar. En lugar de mirar un fragmento de código, contar en tu cabeza y usar cualquiera de estas combinaciones para realizar alguna acción:

```text
{operator}{count}{motion}
```

o moverse:

```text
{count}{motion}
```

cuando activa un movimiento con EasyMotion, etiqueta los posibles objetivos en todo el documento con una combinación de teclas que se muestran en una superposición (sobre el texto en cuestión). Escribe esa combinación de teclas y te teletransportarás a esa ubicación de inmediato.

Por ejemplo, escribe **`<Leader><Leader>w`** y EasyMotion etiquetará el comienzo de todas las siguientes palabras de la siguiente manera:

![Pasar al comienzo de las palabras en movimiento fácil](https://www.barbarianmeetscoding.com/images/vscodevim-easymotion.jpg)

*¡Esto es lo que sucede cuando disparas un movimiento con EasyMotion! :O*

En el ejemplo de la imagen, escribir la letra **`l`** haría que el cursor saltara a la `FactionShipModifiers` interfaz, mientras que escribir **`p`** te enviaría a la propiedad `Energy` de esa interfaz.

O puedes escribir **`f'`** y EasyMotion etiquetará todas las apariciones de la tecla **`'`** en las líneas actuales y posteriores. Bastante ingenioso, ¿no?

Todos los movimientos proporcionados por vim-EasyMotion tienen espacios de nombres **`<Leader><Leader>`** y utilizan enlaces de teclas cuyo significado está relacionado con los movimientos principales de Vim:

| mando         | mover a…                                                     |
| :------------ | :----------------------------------------------------------- |
| **`<Leader><Leader>w`**       | comienzo de palabras                                         |
| **`<Leader><Leader>b`**       | comienzo de palabras al revés                                |
| **`<Leader><Leader>bdw`**     | comienzo de palabras en todas partes. Los **`<Leader<Leader>bd`** proviene de bidireccional |
| **`<Leader><Leader>e`**       | fin de las palabras                                          |
| **`<Leader><Leader>ge`**      | fin de las palabras al revés                                 |
| **`<Leader><Leader>edw`**     | fin de las palabras en todas partes                          |
| **`<Leader><Leader>j`**       | comienzo de líneas                                           |
| **`<Leader><Leader>k`**       | comienzo de líneas hacia atrás                               |
| **`<Leader><Leader>f{char}`** | encontrar personaje                                          |
| **`<Leader><Leader>F{char}`** | encontrar el personaje al revés                              |
| **`<Leader><Leader>t{char}`** | hasta el personaje                                           |
| **`<Leader><Leader>T{char}`** | hasta que el personaje retroceda                             |
| **`<Leader><Leader>s{char}`** | buscar personaje en todas partes                             |

### Easymotion solo funciona para moverse

En la versión VSCodeVim, los movimientos en EasyMotion solo admiten moverse y no se pueden combinar con operadores. Esta es una característica que es compatible con el Vim tradicional, por lo que puede ser algo que vendrá con VSCodeVim en el futuro.
