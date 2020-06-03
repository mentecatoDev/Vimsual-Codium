# Integrando vscode con neovim

>>> Advertencia: característica experimental
>>>
>>> Esta es una característica experimental en VSCodeVim. A veces, puede dar lugar a un comportamiento inesperado. Las cosas más nefastas que he visto hacer es mostrar mensajes de error o no hacer lo que le ordené. Ambos son irritantes, pero nada que destruya tu computadora.

Una última forma de mejorar su experiencia VSCodeVim es mediante la integración con Neovim, la bifurcación moderna de Vim. Cuando se integra ambos editores, VSCodeVim usará Neovim para ejecutar todos los *comandos del modo de línea de* comandos. Esto dará como resultado una ejecución de comandos más rápida y la adición de una gran cantidad de comandos útiles a tu arsenal VSCodeVim.

>>> ¿Qué es Neovim?
>>>
>>> Neovim es una bifurcación moderna de Vim que tiene como objetivo refactorizar Vim y hacer que sea más fácil de mantener, extensible y más fácil de contribuir por una comunidad más amplia. Su principal innovación sobre el Vim tradicional fue que soportaba procesamiento asíncrono, un terminal integrado y complementos externos. Vim 8 más tarde se puso al día con soporte para procesamiento asíncrono y un terminal integrado, pero Neovim sigue siendo muy relevante.
>>>
>>> De hecho, sigue siendo muy activo, saludable y supera los límites: su soporte para complementos externos escritos en JavaScript a través de node.js es una gran ayuda para crear una comunidad aún más inclusiva de escritores de complementos. Su modo sin cabeza permite que las aplicaciones GUI (como Visual Studio Code u [Oni](https://www.onivim.io/)) consuman Vim como servicio. Su enfoque como una gran experiencia de usuario ha traído nuevas características interesantes a Vim, como líneas virtuales con mensajes en el editor, tal como lo que se espera de los editores de texto modernos. Finalmente, sus valores predeterminados más sensibles lo convierten en un editor más accesible que el Vim original.
>>>
>>> Además, la mera existencia de Neovim como competidor de Vim es algo saludable para la comunidad en general. Por ejemplo, características como el terminal integrado o el procesamiento asíncrono se agregaron a Vim después de que estuvieron disponibles en Neovim.
>>>
>>> Puedes encontrar más información sobre Neovim en [neovim.io](https://neovim.io/).

## Instalando neovim

Neovim, al igual que Vim, es compatible con [muchos sistemas operativos](https://github.com/neovim/neovim/wiki/Installing-Neovim) . Para instalar Neovim, usa el administrador de paquetes favorito de tu sistema operativo de elección. Por ejemplo:
### Instalar neovim en Arch

Para instalar la última versión de Neovim en Arch y derivadas (Arcolinux, Manjaro...) usa lo siguiente:

```bash
$ pacman -S neovim
```

### Instalar neovim en ubuntu o debian

Para instalar la última versión de Neovim en Ubuntu o Debian usa lo siguiente:

```bash
$ sudo apt-get update
$ sudo apt-get install software-properties-common -y
$ sudo add-apt-repository ppa:neovim-ppa/stable
$ sudo apt-get update
$ sudo apt-get install neovim -y
```

### Instalar neovim en mac osx

La forma más sencilla de obtener Neovim en OSX es usar [Homebrew](https://brew.sh/) :

```bash
$ brew install neovim
```

### Instalar neovim en windows

La forma más sencilla de instalar Neovim en Windows es usar el administrador de paquetes [Chocolatey](https://chocolatey.org/). Escribe:

```powershell
PS> choco install neovim -y
```

### Instalar neovim en otros sistemas operativos

El [Wiki de Neovim](https://github.com/neovim/neovim/wiki/Installing-Neovim) tiene instrucciones detalladas sobre cómo instalar Neovim en muchos sistemas operativos, utilizando un administrador de paquetes o construyendolo desde la fuente. Si tu sistema operativo no es uno de los anteriores, teletransportate a [la Wiki de Neovim](https://github.com/neovim/neovim/wiki/Installing-Neovim) y sigue las instrucciones.

## Habilitar neovim dentro de vscode

Una vez que hayas instalado Neovim en tu sistema operativo, puedes habilitarlo dentro de VSCode desde la ventana *Preferences: Settings*: 

1. Habilita la opción *Vim: Enable Neovim* ( `vim.enableNeovim`)
2. Establezca el camino a Neovim dentro de la configuración *Vim: Neovim Path* (`vim.neovimPath`) al valor de tu sistema (típicamente /usr/bin/nvim)
3. Reiniciar VSCode

Por ejemplo, si estás usando Arch, tu configuración se vería así:

```json
{
  "vim.neovimPath": "/usr/bin/nvim",
  "vim.enableNeovim": true
}
```

## Usando el Neovim de VSCode

Una vez que se habilita la integración, cada vez que ejecutes un comando Ex, se ejecutará dentro de Neovim y sus efectos se reflejarán en Visual Studio Code. En esencia, la ejecución de un comando Ex seguirá estos pasos:

1. Copia el contenido de tu archivo dentro de Neovim.
2. Ejecuta el comando en Neovim.
3. Vuelve a sincronizar los resultados con Visual Studio Code.

Esto significa que los comandos interactivos como **`:change`** (o **`substitute`** con la bandera **`c`**) no funcionará con el estado actual experimental de esta integración, pero otros como **`:move`**, **`:normal`**, **`:global`**, y la mayoría de los casos de uso de **`:substitute`**trabajo fino voluntad.

## Copiar y mover líneas alrededor

Con los comandos **`:copy`** o **`:move`** puedes copiar o mover rápidamente un rango de líneas de una parte del documento a otra. Utiliza cualquiera de estos comandos de la siguiente manera:

```vim
:[range]copy {address}
:[range]move {address}
```

Donde:

- **`range`** define el rango que queremos copiar o mover.
- **`address`** define el destino de la línea objetivo de lo que copiamos o movemos.

Por ejemplo:

- **`:,+3c $`** copia la línea actual y las 3 líneas siguientes al final del archivo.
- **`:,+3m $`** como arriba pero mueve las líneas en su lugar.

Ambos comandos admiten atajos:

- **`:t`** o **`:co`** son equivalentes a **`:copy`**.
- **`:m`** es equivalente a **`:move`**.

## El comando normal

El comando **`:normal`** (abreviatura **`:norm`**) te permite **ejecutar una colección arbitraria de comandos del modo Normal en varias líneas a la vez**. Se define así:

```vim
:[range]normal {commands}
```

Imagina que encuentras un archivo JavaScript cuyas líneas no tienen punto y coma. ¡Oh no! ¡Malditos hipsters JavaScript!. Puedes remediar esta parodia usando el comando **`:normal`** de esta forma:

```vim
:%norm A;
```

Que agrega punto y coma a todas las líneas dentro de un archivo. Esta es, sin lugar a dudas, una forma más rápida de agregar punto y coma que usar:

1. Para **`A;`** agregar un punto y coma, en combinación con,
2. los comandos **`j.`** para bajar una línea y repetir el último cambio.

Veamos un ejemplo un poco más complicado. Imagina que tienes una lista de armas mágicas que se viera así:

```html
<ul>
  <li>Sword of Truth</li>
  <li>Fire Lance</li>
  <li>Shardblade</li>
  <li>Poisoned Dagger of Despair</li>
</ul>
```

Pero ahora queremos mejorar la utilidad de esta lista y agregar algunos enlaces a lugares de Wizardsphere donde alguien podría adquirir algunos de estos elementos.

Simplifiquemos el problema agregando un enlace a un solo elemento  **`li`**:

```html
  <li>Sword of Truth</li>
^
```

Podríamos **`w`** para mover el cursor sobre el elemento y **`cit`** cambiar su contenido. Ahora escribe **`<a href=""><ESC>`**:

```html
  <li><a href=""></li>
                ^
```

Luego, usa **`p`** para pegar los contenidos anteriores de **`li`**:

```html
  <li><a href="">Sword of Truth</li>
                              ^
```

Y finalmente **`a`**:

```html
  <li><a href="">Sword of Truth</a></li>
                                  ^
```

¡Tada! La serie completa de comandos fue:

```text
wcit<a href=""><ESC>pa</a><ESC
```

Así que, ahora que hemos resuelto este problema para una sola línea, deberíamos poder aplicar el mismo comando a todos los elementos **`li`** de nuestra lista aprovechando el comando **`:normal`**:

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

¿Puedes ver el problema? ¡Exactamente! Todos los caracteres han sido tomados literalmente. El **`<ESC>`** no funcionó y, por lo tanto, nunca salimos del *modo Insertar*, que explica los resultados anteriores.

Esto muestra una de las limitaciones del comando **`:normal`**: no comprende teclas especiales como **`<ENTER>`** o acordes **`<C->`**. Afortunadamente, hay una manera de resolver estos casos de uso con la ayuda del comando **`:execute`**.

El comando **`:execute`** (abreviatura **`:exe`**) te permite evaluar una expresión de cadena como un comando ex. Es como el **`eval`** de Vim. Usando **`:execute`** podemos usar el comando **`:normal`** junto con teclas especiales de la siguiente manera:

```text
:execute "%normal wcit<a href=\"\">\<ESC>pa</a>\<ESC>"
```

Observa cómo los comandos de ejecución nos permiten usar teclas especiales, como **`<ESC>`** escapándolas con una barra diagonal inversa. Observa también cómo, debido a que toda la expresión es una cadena, debemos escapar de las comillas dobles que puedan aparecer.

En resumen:

- El comando **`:normal`** te permite aplicar comandos arbitrarios de *modo Normal* en varias líneas a la vez. Sin embargo, por sí solo, no admite teclas especiales, lo que limita su uso.
- Úsa **`:normal`** en combinación con el comando **`:execute`** cuando tu secuencia de comandos de modo normal incluya teclas especiales

## El comando global

El comando **`:global`** (abreviatura **`:g`**) te permite **ejecutar cualquier comando Ex en líneas que coincidan con un patrón dado**. Es como una versión genérica de **`:s`** que, en lugar de simplemente sustituir un patrón por otra cosa, te permite hacer casi cualquier cosa.

La forma del comando **`:global`** debería serte familiar en este momento:

```text
:[range]g[lobal]/{pattern}/[cmd]
```

Así:

- Se define un lugar **`range`** donde aplicar el comando **`:g`** y luego,
- dentro de ese rango, el comando **`cmd`** se aplicará solo a aquellas líneas que coincidan con el **`pattern`**.

El rango predeterminado para el comando **`:g`** es todo el documento, por lo que **`:g`** es equivalente a **`:1,$g`** o **`:%g`**. Esto es apropiado: justamente el comando se llama *global* por algo.

Con el comando **`:global`** ahora podemos eliminar o copiar líneas que coinciden con un patrón específico. Por ejemplo, podemos crear un esquema de un documento de descuento copiando (tirando) todos los títulos y almacenándolos en un registro de la siguiente manera:

```vim
:g/^#/y A
```

Lo que significa que:

- para cada línea que coincida con este patrón **`^#`** (un título resumido),
- ejecuta el comando **`:y A`**, que significa: Copia la línea actual y añádela al registro **`a`** (¿recuerdas? Un registro en mayúscula significa usarla para agregar en lugar de reemplazar su contenido).

Ahora puedes pegar el contorno en otro archivo escribiendo **`:put a`** (o simplemente **`"ap`** en *modo Normal* ).

El comando **`:global`** es especialmente útil cuando se combina con el comando **`:normal`** porque te permite **ejecutar un número arbitrario de comandos en \*modo Normal\* solo cuando se cumple una determinada condición**.

Por lo tanto, podríamos refinar nuestro dispositivo de adición de punto y coma anterior para agregar solo un punto y coma cuando no encuentre uno al final de una línea de esta manera:

```vim
:g!/;$/norm A;
```

O podríamos definir un comando que disminuya la profundidad de los capítulos de reducidos como este:

```vim
:g/^#/norm 0x
```

Usando los comandos **`:global`** y **`:normal`** juntos, el único límite de lo que puedes lograr está determinado por tu propia imaginación.

>>> `global` vs `global!`
>>>
>>> ¿Notaste el `:g!` del ejemplo anterior? Cuando usamos `:global!` en lugar del comando Ex `:global` que definimos, se aplica solo en las líneas que **no** coinciden con el patrón que especificamos.

## Una advertencia de eliminación a tener en cuenta

Cuando habilites la integración de Neovim, el comando **`:delete`** se ejecutará dentro de Neovim y usará sus registros. Estos registros no se comparten con VSCodeVim y, por lo tanto, no podrás inspeccionarlos mediante el comando `:reg`. No obstante, puedes confiar en el hecho de que todavía están allí. Así que la siguiente secuencia funcionará como se espera:

1. `:0,+3d a` elimina las primeras tres líneas en el registro `a`
2. `:$put a` pega el contenido del registro `a` (las tres líneas que eliminamos anteriormente) al final del archivo