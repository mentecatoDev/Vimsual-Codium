# ELEVANDO SU FLUJO DE TRABAJO CON ASIGNACIONES PERSONALIZADAS

Una de las mejores características de Vim es su personalización. Una forma sencilla de comenzar a personalizar Vim y una que tendrá el mayor efecto en su codificación diaria es **crear asignaciones personalizadas** . Un mapeo en Vim es el equivalente a un atajo en otros editores pero con un fuerte enfoque en las melodías de teclas que son tan naturales para Vim.

## ¿POR QUÉ MAPEOS PERSONALIZADOS?

Las asignaciones personalizadas son útiles por dos razones:

1. Le permiten personalizar Vim y adaptarlo a su forma de trabajo mediante la creación de asignaciones personalizadas para las cosas que utiliza con frecuencia.
2. Le permiten priorizar la funcionalidad de Vim acercándola a su alcance. Mediante el uso de asignaciones personalizadas, puede crear una jerarquía de comandos donde se puede acceder a los más útiles desde el producto de su fila de inicio y a los menos útiles a través de combinaciones de teclas cómodas, pero más largas

## CREAR ASIGNACIONES PERSONALIZADAS

Puede crear asignaciones personalizadas utilizando las preferencias de Visual Studio Code:

1. Abra la paleta de comandos con **`CMD-SHIFT-P`**o**`CTRL-SHIFT-P`**
2. Preferencias de tipo
3. Seleccione las *preferencias: abrir las opciones de configuración del usuario*
4. Tipo **`vim`**

Y filtrará sus preferencias de Visual Studio Code para mostrar solo las relacionadas con VSCodeVim. Ahora puede usar la siguiente configuración para agregar sus asignaciones personalizadas en diferentes modos:

- *Asignaciones de teclas* en modo normal *No recursivas* para modo normal
- *Enlaces de teclas del modo visual No recursivo* para el modo visual
- *Vinculaciones de teclas del modo de inserción No recursivo* para el modo de inserción

Tener diferentes asignaciones para diferentes modos tiene sentido porque cada modo es una pizarra limpia donde puede redefinir asignaciones para realizar tareas específicas de ese modo. Eso le permite reutilizar el teclado del estado real del teclado en cada modo y tener una funcionalidad potente cerca de sus dedos.

Tenga en cuenta que esta configuración solo se puede cambiar a través de la **`json`**versión de la configuración:

![Crear asignaciones personalizadas en VSCodeVim](/home/pater/Dropbox/apuntes/vsc/img/vim-custom-mappings.jpg)

Un mapeo personalizado normalmente toma la siguiente forma:

```json
{
  "vim.insertModeKeyBindingsNonRecursive": [
    {
      "before": ["j", "k"],
      "after": ["<ESC>"]
    }
  ],
}
```

Dónde:

- **antes** es la secuencia de comandos que escribe.
- **después** es a qué se asignan los comandos anteriores y qué se ejecuta cuando los escribe.

En el ejemplo anterior, cada vez que escribimos la secuencia **`jk`**en *modo Insertar* será el equivalente a escribir **``**y, por lo tanto, nos llevará de vuelta al *modo Normal* . Esta es una gran asignación personalizada que hace una tarea sin fisuras muy común, ya que ambos **`j`**y **`k`**están en la fila casa y sólo por debajo de su mano derecha.

Agregue esta asignación a su configuración y verá que surte efecto tan pronto como guarde su configuración. Ahora intente ir al *modo Insertar* y escriba **`jk`**una sucesión rápida. **`ijk`**, **`ijk`**, **`ijk`**... Se debe fluir suavemente como una corriente pacífica o como la mantequilla caliente sobre una tostada.

## PAUTAS PARA CREAR ASIGNACIONES PERSONALIZADAS

La capacidad de crear asignaciones personalizadas le brinda mucha libertad y flexibilidad para definir cómo interactúa con Visual Studio Code. Pero debido a que no hay nada que lo detenga por hacer lo que quiera, puede terminar pegándose un tiro en el pie. Aquí hay algunas reglas que lo guiarán cuando cree sus propios mapeos personalizados y guarde esos preciosos dedos de los suyos:

- En general, use la tecla **líder** para definir sus asignaciones personalizadas. La clave **líder** es una clave especial en Vim cuyo propósito es actuar como un espacio de nombres o puerta de enlace a las asignaciones definidas por el usuario. De manera predeterminada, la tecla líder se asigna a la tecla de barra diagonal inversa **`\`**.
- Si hay algo en su flujo de trabajo que usa todo el tiempo, entonces está bien (de hecho se recomienda) sobrescribir un enlace Vim predeterminado menos útil. Esta es la excepción a la regla.
- Crea asignaciones que sean fáciles de recordar. Sigue la tradición de Vim y confía en la mnemotecnia. (Recuerde? `c`Para **c** ambio, `d`para **d** elete, y tal ...)

Si estas reglas parecen demasiado abstractas, no se preocupe, en las siguientes secciones las haremos más prácticas ya que definimos una serie de asignaciones personalizadas que puede agregar a su propia configuración VSCodeVim.

## PERSONALIZAR LA CLAVE DE LÍDER

Puede cambiar la clave de líder a algo más fácil de escribir que la barra invertida **`\`**(no lo conozco, pero odio tener teclas importantes asociadas a mis dedos meñiques [meñique](https://www.barbarianmeetscoding.com/boost-your-coding-fu-with-vscode-and-vim/elevating-your-worflow-with-custom-mappings/#fn-pinky) ). Mi favorito personal es la barra espaciadora, que es muy conveniente para escribir con ambas manos.

Vaya a sus preferencias de VSCode y actualice la siguiente configuración:

```json
{
"vim.leader": "<Space>",
}
```

De ahora en adelante, cada vez que vea un mapeo personalizado que se refiera a **``**usted, puede traducirlo en su cabeza **``**.

## ALGUNAS BUENAS ASIGNACIONES PERSONALIZADAS

Aquí hay algunos otros excelentes ejemplos de mapeos útiles:

### MOVERSE HACIA ARRIBA Y HACIA ABAJO MÁS RÁPIDO EN MODO NORMAL

Estas asignaciones le permiten moverse hacia arriba y hacia abajo más rápido en *modo Normal* (aunque son igual de útiles en *modo Visual* ):

```json
{
  "vim.normalModeKeyBindingsNonRecursive": [
    {
      "before": ["J"],
      "after": ["5", "j"]
    },
    {
      "before": ["K"],
      "after": ["5", "k"]
    },
  ]
}
```

De ahora en adelante podrás usar:

- **`J`** bajar más rápido
- **`K`** subir más rápido

Esto coincide perfectamente con la idea de Vim de que los comandos en mayúsculas sean versiones *más fuertes* de los comandos en minúsculas. Es decir, le **`J`**permite moverse más rápido **`j`**y **`K`**más rápido que **`k`**.

Aquí hemos sobrescrito dos enlaces predeterminados de Vim porque navegar por el código hacia arriba y hacia abajo es algo que harás todo el tiempo. Mientras que **`J`**(unir líneas), aunque es útil, es algo que solo haces de vez en cuando. **`K`**se usa para la búsqueda de palabras clave pero aún no se implementa en VSCodeVim.

### SEGUIR UNIENDO LÍNEAS

Unir líneas sigue siendo útil, así que vamos a mantenerlo. Aunque rebajaremos su importancia en la jerarquía haciéndolo un poco más difícil de escribir.

Actualice su configuración de VSCodeVim para incluir esta nueva asignación:

```json
{
  "vim.normalModeKeyBindingsNonRecursive": [
    {
      "before": ["<Leader>", "j"],
      "after": ["J"]
    },
  ]
}
```

Entonces, cada vez que escriba **`j`**, Vim lo traducirá **`J`**y unirá dos líneas. ¡Pruébalo!

**`j`**no es tan rápido como simplemente escribir, **`J`**pero es lo suficientemente bueno en función de la frecuencia con la que unirá líneas. La mnemónica en este caso es **j** jin.

### CAMBIO MÁS FÁCIL ENTRE DIVISIONES

Cambiar ventanas divididas es algo que harás todo el tiempo, así que prueba estos enlaces:

```json
{
  "vim.normalModeKeyBindingsNonRecursive": [
    {
      "before": ["<C-h>"],
      "after": ["<C-w>", "h"]
    },
    {
      "before": ["<C-j>"],
      "after": ["<C-w>", "j"]
    },
    {
      "before": ["<C-k>"],
      "after": ["<C-w>", "k"]
    },
    {
      "before": ["<C-l>"],
      "after": ["<C-w>", "l"]
    }]
}
```

Te harán mucho más rápido y ágil cuando atravieses divisiones porque requieren una pulsación de tecla menos.

### MANEJO DE PESTAÑAS MÁS FÁCIL

La única forma de interactuar con pestañas en VSCodeVim es a través de comandos que requieren que escriba dos puntos seguidos de un montón de letras.

Podemos hacerlo mejor:

```json
{
  "vim.normalModeKeyBindingsNonRecursive": [
    {
      "before": ["<Leader>", "t", "t"],
      "commands": [":tabnew"]
    },
    {
      "before": ["<Leader>", "t", "n"],
      "commands": [":tabnext"]
    },
    {
      "before": ["<Leader>", "t", "p"],
      "commands": [":tabprev"]
    },
    {
      "before": ["<Leader>", "t", "o"],
      "commands": [":tabo"]
    }]
}
```

Aprovechando la **``**clave, ahora podemos abrir nuevas pestañas, movernos y cerrar todas las pestañas excepto la actual.

**¿Notó algo diferente acerca de estas asignaciones personalizadas?**

¡Exactamente! Utiliza una sintaxis ligeramente diferente al asignar teclas a comandos. En lugar de usar **`before`**y **`after`**. Usamos **`before`**y **`commands`**. **`commands`**representar los comandos Ex o los comandos nativos de Visual Studio que deben ejecutarse cada vez que escribimos la asignación de teclas definida por **`before`**.

### LIMPIEZA DE TEXTO RESALTADO

Cuando busque patrones en Vim utilizando los comandos **`/{pattern}`**y **`?{pattern}`**, se resaltarán los patrones coincidentes. Para eliminar los resaltados, puede usar el comando **`:noh`**( *sin resaltado* ).

Esta es una tarea tan común que prefiero la siguiente asignación:

```json
{
  "vim.normalModeKeyBindingsNonRecursive": [
    {
      "before": ["<Leader>", "/"],
      "commands": [":noh"]
    }]
}
```

Ahora puede escribir **`/`**y deshacerse de los resaltados hasta su próxima búsqueda. El mnemónico es el **/** que normalmente se usa para buscar un patrón. Por lo tanto, puede pensar **`/{pattern}`**en algo que hace para comenzar una búsqueda y **`/`**como algo que hace cuando termina una búsqueda.

## CREAR ASIGNACIONES PERSONALIZADAS PARA ACCIONES VSCODE

Otra cosa genial que puede hacer con VSCode es usar asignaciones de Vim que activen los comandos nativos de Visual Studio Code. Por ejemplo, el siguiente enlace:

```json
{
  "vim.normalModeKeyBindingsNonRecursive": [
    {
      "before": ["leader", "w"],
      "commands": [
          "workbench.action.files.save",
      ]
    }
}
```

Vamos a guardar un archivo mediante la **`w`**activación de la `"workbench.action.files.save"`acción VSCode .

### ¿CÓMO ENCONTRAR LOS NOMBRES DE LOS COMANDOS?

Descubrir qué comando hace qué en VSCode no es realmente evidente, es decir, si hubiera querido saber que guardar cosas en VSCode es difícil `workbench.action.files.save`habría adivinado eso. Entonces, ¿dónde puedes encontrar esa información oscura?

Abra la paleta de comandos, escriba *teclado* y seleccione *Preferencias: Abrir atajos de teclado* . Allí encontrará todos los comandos que están disponibles dentro de VSCode, incluido su nombre de comando completo. Úselos siempre que desee crear asignaciones personalizadas para acciones nativas de VSCode.

**Advertencia** : cuando busca un comando, el nombre completo del comando solo se mostrará si la condición del filtro es parte del nombre. Si el nombre del comando no se muestra después del filtrado, puede pasar el mouse sobre el nombre del comando y una información sobre herramientas revelará su nombre completo.

Veamos otro ejemplo. Hay cuatro características en VSCode que encuentro extremadamente útiles:

- La **paleta de comandos** ( `CTRL-SHIFT-P`o `CMD-SHIFT-P`)
- **Ir al archivo** ( `CTRL-P`o `CMD-P`)
- **Ir al símbolo en el archivo** ( `CTRL-SHIFT-O`o `CMD-SHIFT-O`)
- **Ir al símbolo en el espacio de trabajo** ( `CMD-T`o `CTRL-T`)

La *paleta de comandos* y el *símbolo Ir al archivo* son particularmente difíciles de escribir, así que creemos una asignación personalizada para mantener nuestras muñecas saludables:

```json
{
  "vim.normalModeKeyBindingsNonRecursive": [
    {
      "before": ["<Leader>", "p"],
      "commands": [
          "workbench.action.showCommands",
      ]
    },
    {
      "before": ["<Leader>", "t"],
      "commands": [
          "workbench.action.gotoSymbol",
      ]
    }
  ]
}
```

Ahora ya no necesita retorcer los dedos para abrir la *paleta de comandos* o *ir al símbolo* . Simplemente escriba **`p`**y **`t`**respectivamente y accederá rápidamente a cualquiera de estos paneles. Yihoo!

Hay muchas más asignaciones interesantes y útiles en la [documentación de VSCodeVim. ¡Echar un vistazo! ](https://github.com/VSCodeVim/Vim#key-remapping). Pero recuerda ser crítico. Antes de agregar un mapeo personalizado en su configuración de VSCodeVim, considere si ofrece un mejor flujo de trabajo que el que usa actualmente. Nunca agregue cosas a su configuración a ciegas.

**Una parte importante de ser más eficaz con Vim es tener en cuenta su flujo de trabajo de desarrollo. Revisando su configuración de Vim de vez en cuando, y agregando nuevas asignaciones que mejoran su forma de trabajar. Por lo tanto, tenga en cuenta a partir de ahora y mantenga su configuración Vim muy nítida.**