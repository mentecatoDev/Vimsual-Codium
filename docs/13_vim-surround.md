# Cosas circundantes con vim surround

VSCodeVim viene con un montón de complementos útiles de Vim integrados. Uno de ellos es [vim-surround,](https://github.com/tpope/vim-surround) que está habilitado de forma predeterminada y extiende el lenguaje secreto de Vim con un nuevo operador: **surround** o **`s`**.

Usando el operador de "sonido" envolvente podemos operar en los alrededores (comillas, paréntesis, llaves, etiquetas, etc.) de franjas de texto de la misma manera que utilizamos otros operadores dentro de Vim.

El operador envolvente en sí mismo puede verse como tres operadores separados:

- **`ds`** para eliminar los alrededores
- **`cs`** para cambiar el entorno
- **`ys`** para agregar alrededores

Y así, como cualquier operador en Vim, se usarían así:

```text
ds{count}{motion}
cs{count}{motion}
ys{count}{motion}
```

Por ejemplo:

- **`ds'`** para eliminar el entorno **`'`** (`ds{char}`)
- **`cs'"`** cambiar el entorno **`'`** para **`"`** (`cs{old}{new}`)
- **`ysaptli>`** para rodear un párrafo con un **t**ag `<li>` (`ys{motion}{char}`)

¿Recuerda que siempre puedes usar el comando **`.`** para repetir el último cambio? ¿Deseas rodear varios elementos de texto con un elemento **`<li>`**? Puedes escribir **`ysaptli>`** la primera vez y luego **`.`** las siguientes.

También puedes usar *vim-surround* seleccionando un poco de texto en modo visual y luego usándolo `S{desired character}`. Esto rodeará tu selección de texto con el carácter deseado.

Inténtalo. Te ahorrará mucho de tiempo.
