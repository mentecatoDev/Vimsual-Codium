# INTEGRANDO VSCODE CON NEOVIM

### ADVERTENCIA: CARACTERÍSTICA EXPERIMENTAL

Esta es una característica experimental en VSCodeVim. A veces, puede dar lugar a un comportamiento inesperado. Las cosas más nefastas que he visto hacer es mostrar mensajes de error o no hacer lo que le ordené. Ambos son irritantes, pero nada que destruya su computadora.

Una última forma de mejorar su experiencia VSCodeVim es mediante la integración con Neovim, la bifurcación moderna de Vim. Cuando integra ambos editores, VSCodeVim usará Neovim para ejecutar todos los *comandos del modo de línea de* comandos. Esto dará como resultado una ejecución de comandos más rápida y la adición de una gran cantidad de comandos útiles a su arsenal VSCodeVim.

### ¿QUÉ ES NEOVIM?

Neovim es una bifurcación moderna de Vim que tiene como objetivo refactorizar Vim y hacer que sea más fácil de mantener, extensible y más fácil de contribuir por una comunidad más amplia. Su principal innovación sobre Vim tradicional fue que soportaba procesamiento asíncrono, un terminal integrado y complementos externos. Vim 8 más tarde se puso al día con soporte para procesamiento asíncrono y un terminal integrado, pero Neovim sigue siendo muy relevante.

De hecho, Neovim sigue siendo muy activo, saludable y supera los límites: su soporte para complementos externos escritos en JavaScript a través de node.js es una gran ayuda para crear una comunidad aún más inclusiva de escritores de complementos. Su modo sin cabeza permite que las aplicaciones GUI (como Visual Studio Code u [Oni](https://www.onivim.io/) ) consuman Vim como servicio. Su enfoque en una gran experiencia de usuario ha traído nuevas características interesantes a Vim, como líneas virtuales con mensajes en el editor, tal como lo que espera de los editores de texto modernos. Finalmente, sus valores predeterminados más sensibles lo convierten en un editor más accesible que el Vim original.

Además, la mera existencia de Neovim como competidor de Vim es algo saludable para la comunidad en general. Por ejemplo, características como el terminal integrado o el procesamiento asíncrono se agregaron a Vim después de que estuvieron disponibles en Neovim.

Puede encontrar más información sobre Neovim en [neovim.io](https://neovim.io/) .

## INSTALANDO NEOVIM

Neovim, al igual que Vim, es compatible con [muchos sistemas operativos](https://github.com/neovim/neovim/wiki/Installing-Neovim) . Para instalar Neovim, use el administrador de paquetes favorito de su sistema operativo de elección. Por ejemplo:

### INSTALAR NEOVIM EN MAC OSX

La forma más sencilla de obtener Neovim en OSX es usar [Homebrew](https://brew.sh/) :

```bash
$ brew install neovim
```

### INSTALAR NEOVIM EN WINDOWS

La forma más sencilla de instalar Neovim en Windows es usar el administrador de paquetes [Chocolatey](https://chocolatey.org/) . Tipo:

```powershell
PS> choco install neovim -y
```

### INSTALAR NEOVIM EN UBUNTU O DEBIAN

Para instalar la última versión de Neovim en Ubuntu o Debian use lo siguiente:

```bash
$ sudo apt-get update
$ sudo apt-get install software-properties-common -y
$ sudo add-apt-repository ppa:neovim-ppa/stable
$ sudo apt-get update
$ sudo apt-get install neovim -y
```

### INSTALE NEOVIM EN OTROS SISTEMAS OPERATIVOS

El [Wiki de Neovim](https://github.com/neovim/neovim/wiki/Installing-Neovim) tiene instrucciones detalladas sobre cómo instalar Neovim en muchos sistemas operativos, utilizando un administrador de paquetes o construyendo desde la fuente. Si su sistema operativo no es uno de los anteriores, teletransportarse a [la Wiki de Neovim](https://github.com/neovim/neovim/wiki/Installing-Neovim) y seguir las instrucciones.

## HABILITAR NEOVIM INSIDE VSCODE

Una vez que haya instalado Neovim en su sistema operativo, puede habilitarlo dentro de VSCode dentro de la ventana *Preferencias: Configuración de usuario* :

1. Habilite la opción *Vim: Habilitar Neovim* ( `vim.enableNeovim`)
2. Establezca el camino a Neovim dentro de la configuración *Vim: Neovim Path* ( `vim.neovimPath`)
3. Reiniciar VSCode

Por ejemplo, si está usando MacOS y ha instalado Neovim usando brew, su configuración se vería así:

```json
{
  "vim.neovimPath": "/usr/local/bin/nvim",
  "vim.enableNeovim": true
}
```

## USANDO NEOVIM DE VSCODE

Una vez que se habilita la integración, cada vez que ejecute un comando Ex, se ejecutará dentro de Neovim y luego sus efectos se reflejarán en Visual Studio Code. En esencia, la ejecución de un comando Ex seguirá estos pasos:

1. Copie el contenido de su archivo dentro de Neovim.
2. Ejecute el comando en Neovim.
3. Vuelva a sincronizar los resultados con Visual Studio Code.

Esto significa que los comandos interactivos como **`:change`**(o **`substitute`**con la **`c`**bandera) no funcionará con el estado actual experimental de esta integración, pero otros como **`:move`**, **`:normal`**, **`:global`**, y la mayoría de los casos de uso de **`:substitute`**trabajo fino voluntad.

## COPIAR Y MOVER LÍNEAS ALREDEDOR

Con los comandos **`:copy`**o **`:move`**puede copiar o mover rápidamente un rango de líneas de una parte del documento a otra. Utiliza cualquiera de estos comandos de la siguiente manera:

```vim
:[range]copy {address}
:[range]move {address}
```

Dónde:

- **`range`** define el rango que queremos copiar o mover.
- **`address`** define el destino de la línea objetivo de lo que copiamos o movemos.

Por ejemplo:

- **`:,+3c $`** copie la línea actual y las 3 líneas siguientes al final del archivo.
- **`:,+3m $`** como arriba pero mueve las líneas en su lugar.

Ambos comandos admiten shorthands:

- **`:t`**o **`:co`**son equivalentes a **`:copy`**.
- **`:m`**es equivalente a **`:move`**.

## EL COMANDO NORMAL

El **`:normal`**comando (abreviatura **`:norm`**) le permite **ejecutar una colección arbitraria de comandos del modo Normal en varias líneas a la vez** . Se define así:

```vim
:[range]normal {commands}
```

Imagine que encuentra un archivo JavaScript cuyas líneas no tienen punto y coma. ¡Oh no! ¡Malditos hipsters JavaScript! [broma](https://www.barbarianmeetscoding.com/boost-your-coding-fu-with-vscode-and-vim/integrating-vscode-with-neovim/#fn-joke) Puedes remediar esta parodia usando el **`:normal`**comando como este:

```vim
:%norm A;
```

Que agrega punto y coma a todas las líneas dentro de un archivo. Esta es, sin lugar a dudas, una forma más rápida de agregar punto y coma que usar:

1. Para **`A;`**agregar un punto y coma, en combinación con,
2. los **`j.`**comandos para bajar una línea y repetir el último cambio.

Veamos un ejemplo un poco más complicado. Imagina que tienes una lista de armas mágicas que se ve así:

```html
<ul>
  <li>Sword of Truth</li>
  <li>Fire Lance</li>
  <li>Shardblade</li>
  <li>Poisoned Dagger of Despair</li>
</ul>
```

Pero ahora queremos mejorar la utilidad de esta lista y agregar algunos enlaces a lugares de Wizardsphere donde alguien podría adquirir algunos de estos elementos.

Simplifiquemos el problema agregando un enlace a un solo **`li`**elemento:

```html
  <li>Sword of Truth</li>
^
```

Podríamos **`w`**mover el cursor sobre el elemento y **`cit`**cambiar su contenido. Ahora escriba **`[`]()**:

```html
  <li><a href=""></li>
                ^
```

Luego, **`p`**para pegar los contenidos anteriores de **`li`**:

```html
  <li><a href="">Sword of Truth</li>
                              ^
```

Y finalmente **`a`**:

```html
  <li><a href="">Sword of Truth</a></li>
                                  ^
```

Tada! La serie completa de comandos fue:

```text
wcit<a href=""><ESC>pa</a><ESC
```

Entonces, ahora que hemos resuelto este problema para una sola línea, deberíamos poder aplicar el mismo comando a todos los **`li`**elementos de nuestra lista aprovechando el **`:normal`**comando:

```text
:%normal wcit<a href=""><ESC>pa</a><ESC
```

Inténtalo tú mismo. ¿Que pasó? No es lo que esperabas, eso es seguro. Esto debería ser el resultado de ejecutar el comando anterior:

```html
<ul>
  <li><a href=""><ESC>pa</a><ESC></li>
  <li><a href=""><ESC>pa</a><ESC></li>
  <li><a href=""><ESC>pa</a><ESC></li>
  <li><a href=""><ESC>pa</a><ESC></li>
</ul>
```

¿Puedes ver el problema? ¡Exactamente! Todos los personajes han sido tomados literalmente. **``**no funcionó y, por lo tanto, nunca salimos del *modo Insertar,* que explica los resultados anteriores.

Esto muestra una de las limitaciones del **`:normal`**comando: no comprende teclas especiales como **``**o **``**acordes. Afortunadamente, hay una manera de resolver estos casos de uso con la ayuda del **`execute`**comando.

El **`:execute`**comando (abreviatura **`:exe`**) le permite evaluar una expresión de cadena como un ex comando. Es como el **`eval`**de Vim. Usando **`:execute`**podemos usar el **`:normal`**comando junto con teclas especiales de la siguiente manera:

```text
:execute "%normal wcit<a href=\"\">\<ESC>pa</a>\<ESC>"
```

Observe cómo los comandos de ejecución nos permiten usar teclas especiales, como **``**escapándolos con una barra diagonal inversa. Observe también cómo, debido a que toda la expresión es una cadena, debemos escapar de las comillas dobles que puedan aparecer.

En resumen:

- El **`:normal`**comando le permite aplicar comandos arbitrarios de *modo Normal* en varias líneas a la vez. Sin embargo, por sí solo, in no admite teclas especiales, lo que limita su uso.
- Úselo **`:normal`**en combinación con el **`:execute`**comando cuando su secuencia de comandos de modo normal incluye teclas especiales

## EL COMANDO GLOBAL

El **`:global`**comando (abreviatura **`:g`**) le permite **ejecutar cualquier comando Ex en líneas que coinciden con un patrón dado** . Es como una versión genérica de **`:s`**eso, en lugar de simplemente sustituir un patrón por otra cosa, le permite hacer casi cualquier cosa.

La forma del **`:global`**comando debería serle familiar en este momento:

```text
:[range]g[lobal]/{pattern}/[cmd]
```

Entonces:

- Define un lugar **`range`**donde aplicar el **`:g`**comando y luego,
- dentro de ese rango, el comando **`cmd`**se aplicará solo a aquellas líneas que mucho se den **`pattern`**.

El rango predeterminado para el **`:g`**comando es todo el documento, por lo que **`:g`**es equivalente a **`:1,$g`**o **`:%g`**. Esto es apropiado ya que el comando no se llama *global* por nada.

Con el **`:global`**comando ahora podemos eliminar o copiar líneas que coinciden con un patrón específico. Por ejemplo, podemos crear un esquema de un documento de descuento copiando (tirando) todos los títulos y almacenándolos en un registro de la siguiente manera:

```vim
:g/^#/y A
```

Lo que significa:

- Para cada línea que coincida con este patrón **`^#`**(un título en reducción).
- Ejecute el **`:y A`**comando, que significa: Copie la línea actual y añádala al registro **`a`**(¿recuerda? Un registro en mayúscula significa usarla para agregar en lugar de reemplazar su contenido).

Ahora puede pegar el contorno en otro archivo escribiendo **`:put a`**(o simplemente **`"ap`**en *modo Normal* ).

El **`:global`**comando es especialmente útil cuando lo combina con el **`:normal`**comando porque le permite **ejecutar un número arbitrario de comandos en \*modo Normal\* solo cuando se cumple una determinada condición** .

Por lo tanto, podríamos refinar nuestro dispositivo de adición de punto y coma anterior para agregar solo un punto y coma cuando no encuentre uno al final de una línea de esta manera:

```vim
:g!/;$/norm A;
```

O podríamos definir un comando que disminuya la profundidad de los capítulos de reducción como este:

```vim
:g/^#/norm 0x
```

Usando los comandos **`:global`**y **`:normal`**juntos, el único límite de lo que puedes lograr está determinado por tu propia imaginación.

### GLOBAL VS GLOBAL!

¿Notó el `:g!`del ejemplo anterior? Cuando usamos en `:global!`lugar del `:global`comando Ex que definimos, se aplica solo en las líneas que ** no ** coinciden con el patrón que especificamos.

## UNA ADVERTENCIA DE ELIMINACIÓN PARA TENER EN CUENTA

Cuando habilite la integración de Neovim, el **`:delete`**comando se ejecutará dentro de Neovim y usará sus registros. Estos registros no se comparten con VSCodeVim y, por lo tanto, no podrá inspeccionarlos mediante el `:reg`comando. No obstante, puede confiar en el hecho de que todavía están [allí](https://www.barbarianmeetscoding.com/boost-your-coding-fu-with-vscode-and-vim/integrating-vscode-with-neovim/#fn-there) . Entonces la siguiente secuencia funcionará como se esperaba:

1. `:0,+3d a`eliminar las primeras tres líneas en el `a`registro
2. `:$put a`pegue el contenido del registro `a`(las tres líneas que eliminamos anteriormente) al final del archivo