# Introducción

- **Visual Studio Code** ofrece una experiencia de usuario incomparable con un gran soporte para muchos idiomas y ecosistemas de desarrollo. Viene con excelentes valores predeterminados y es muy fácil de usar y comenzar con él.

- **Vim es asombroso.** Su naturaleza **modal** y sus características de edición de texto lo hacen único entre otros editores. Vim ofrece un nivel completamente diferente de capacidad de edición de texto, velocidad y precisión.

La combinación de ambos no podría ser menos **asombrosamente increíble**.

Al combinar las fortalezas de **Vim** y **Visual Studio Code**, podrás hacer que la interfaz entre tu cerebro y la computadora sea muy delgada, haciendo que tus pensamientos se materialicen perfectamente en código.

Esto es lo que vamos a cubrir:

- ¿Qué es vim? ¿Y por qué usar Vim en VSCode?
- ¿Cómo instalar Vim en VSCode?
- Habilidades básicas para sobrevivir en Vim
- Moviéndote increíblemente rápido con Core Vim Motions
- Edición a la velocidad del pensamiento con operadores y movimientos de Vim
- El lenguaje secreto de Vim
- Insertar texto a la Vim
- Seleccionar texto en modo visual
- Copiar y pegar Aprovechando registros
- Cosas circundantes con Vim Surround
- Mudarse aún más rápido con los plugins Sneak y EasyMotion
- Crear accesos directos personalizados para hacerlo más efectivo
- Sobrecargando múltiples cursores con Vim
- Crear unidades de edición reutilizables con macros
- Integrando VSCode con Neovim para un asombro máximo

Al final, serás capaz de manipulaciones de texto muy precisas y poderosas transformaciones de texto que antes eran inalcanzables para tí. Y con el tiempo, y a medida que practiques y te sientas cómodo con los diferentes comandos de Vim, te volverás más rápido y más competente en la edición que nunca.

> No se asume ningún conocimiento previo de Vim, así que no te preocupes si no estás familiarizado con Vim. Te guiaré a través de todos los conceptos y técnicas que necesitas saber para ser efectivo con Visual Studio Code y Vim.

## ¿Qué es VIM?

[Vi](https://www.vim.org/) es un antiguo editor de texto. Más viejo incluso que [la primera edad del mundo](https://en.wikipedia.org/wiki/Vi). Fue diseñado para trabajar en artilugios llamados *terminales* con la característica muy poco común pero inspirada de **funcionar de manera modal**. Es decir, tiene un modo para **insertar texto**, otro para **editar texto** y uno diferente para **seleccionar texto**, esencialmente.

La última y más famosa encarnación de Vi es [Vim](https://en.wikipedia.org/wiki/Vim_(text_editor)) (**V**i **IM**proved o formalmente **V**i **IM**itation) que funciona con interfaces de texto y gráficas, viene con una gran cantidad de mejoras sobre [vi](https://en.wikipedia.org/wiki/Vim_(text_editor)#Features_and_improvements_over_vi) y es compatible con todas las plataformas conocidas por la humanidad.

Pero el impacto de Vim no se detiene con Vim, **las ideas de Vim son tan notables que han trascendido al editor de Vim y se han propagado a otros editores**. Hoy puedes encontrar modos similares a Vim en casi cualquier editor e IDE que puedas imaginar. Como, apropiadamente, en **Visual Studio Code**.

## ¿Por qué VIM? ¿No es suficiente el código de Visual Studio?

**¿Por qué deberías preocuparte por aprender sobre un antiguo editor en estos tiempos?** ¿Realmente marca una gran diferencia en mi configuración de Visual Studio Code?

La verdad es que Vim proporciona una forma diferente de interactuar con el texto de cualquier otra cosa que hayas visto. Una forma que te brinda **un nivel completamente diferente de control y fluidez al editar código** .

A manos de un usuario experimentado, editar texto con Vim **parece mágico**:

- **Vim te hace más rápido** .
- **Vim te hace más preciso**
- **Vim desbloquea un nivel de control completamente diferente en la edición de texto**
- **Vim adelgaza la interfaz entre tu cerebro y la computadora**
- **Es sorprendente contemplarlo mientras se hacen presentaciones** :D

¡Increíble! Eso suena muy bien y todo eso... Pero... *¿Cómo puede Vim lograr todo esto?* La respuesta es: **modos**.

La naturaleza modal de Vim le permite a tu teclado controlar cada aspecto de tu editor. Cada modo es una pizarra limpia que le da a tu teclado nuevos poderes, para editar texto a la velocidad del rayo, navegar a la velocidad del pensamiento, seleccionar y mover texto al contenido de tu corazón, y más.

Con Vim, ya no estás limitado a insertar texto ni estás sujeto a la tiranía del mouse para hacer clic, navegar o seleccionar texto. No. Después de usar Vim durante un tiempo, **serás como un cirujano de códigos** que realiza incisiones expertas con precisión quirúrgica cuando y donde sea necesario, navegando a través de tu código a la velocidad del rayo y a la precisión de un **flujo de trabajo totalmente controlado por teclado** .

Entonces, **¿por qué querrías aprender Vim hoy en día?**. Parafraseando al poderoso autor [Drew Neil](https://twitter.com/nelstrom) de [Practical Vim](https://amzn.to/2CIzSpb) y maestro de los arcanos más oscuros de Vim:

> Vim is for programmers who want to raise their game. In the hands of an expert, Vim shreds text at the speed of thought.

> Vim es para **programadores que quieren mejorar su juego**. En manos de un experto, **Vim tritura el texto a la velocidad del pensamiento**.

¿Y quién no querría eso?

## ¿Por qué VIM en VSCODE y no solo VIM?

Tal vez te estés preguntando... Ok. Si Vim es tan bueno, entonces... ¿Por qué no usar Vim en lugar de Vim dentro de Visual Studio Code?

¡Gran pregunta! La verdad es que configurar Vim para que funcione con un conjunto de características similar a los editores de texto modernos no es una tarea trivial. Características como la finalización del código, la navegación del código, los mensajes de error en el editor, etc., aunque Vim no lo admite, funcionan perfectamente de forma inmediata.

Visual Studio Code y Vim juntos ofrecen un punto muy dulce que equilibra la facilidad de configuración y la experiencia de usuario de desarrollo súper rica de Visual Studio Code con muchas de las increíbles funciones presentes en Vim.

Sin embargo, la traducción aún no es perfecta. Y si eres un usuario experimentado de Vim, es posible que falten algunas funciones. Pero en general, VSCodeVim ofrece una experiencia de Vim muy agradable fuera de Vim.

## Una breve nota sobre las convenciones utilizadas

Dado que mucho de lo que sucede en Vim depende de la ubicación del cursor, he usado una serie de diagramas que muestran la posición del cursor y cómo cambia con el tiempo a medida que escribes comandos. Y dado que es bastante poco convencional frente a otros libros de programación, creo que te será útil que te lo explique para que estés preparado antes de que te lo encuentres por primera vez. Aquí hay un ejemplo:


```text
wwww ==> v   v v  v   v
         word. is two words
```

Eso significa lo siguiente:

```text
  comandos tecleándose    posición del cursor
   /                    /   cambiando mientras
  /                    /    se teclea
wwww ==> v      v v   v   v  
         Palabra. Son dos palabras
           /
          /
      texto en el editor
```

Entonces:

- El texto `Palabra. Son dos palabras` es el texto que está dentro de tu editor y que está sujeto a cambios o navegación.
- Escribe el comando `w` sucesivamente (en este caso 4 veces)
- Cada vez que escribes el comando, se mueve el cursor (representado por `v`) a una nueva ubicación

A veces, será útil comparar cómo funcionan dos comandos cuando se aplican sobre el mismo trozo de texto. En esos casos he usado los siguientes diagramas:

```text
wwww ==> v      v v   v   v
         palabra. Son dos palabras
         palabra. Es una PALABRA
WWW  ==> ^        ^  ^   ^
```

Donde la parte inferior es similar en significado a la parte superior que discutimos anteriormente, pero por el hecho de que el cursor está representado por un cursor en forma de `^` en lugar de `v`.

Al explicar los comandos, prestaremos atención a las siguientes convenciones. Para operaciones y movimientos:

```text
f{character}

f            - f es el literal f, tal y como es
{character}  - es el lugar que necesita ser sustituido
               por algo. El nombre entre {} describe
               lo que se supone que debe aparecer.
               En este caso, un carácter.
```

Al construir y aplicar objetos de texto:

```text
{operator}{a|i}{text-object}

{operator}    - marcador de posición
{a|i}         - elegir entre la letra "a" ó "i"
{text-object} - otro marcador de posición
```

Y para ex-comandos:

```text
:[range]s/{pattern}/{substitute}/[flags]

:            - marca el comienzo de un comando ex.
[range]      - [] denota que esta parte es opcional.
               El nombre será descriptivo
s            - comando literal.
{pattern}    - marcador de posición.
{substitute} - otro marcador de posición.
[flags]      - otra parte opcional.
```