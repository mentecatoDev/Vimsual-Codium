# Operando como un rayo con coincidencias de búsqueda

Anteriormente, aprendiste cómo puedes usar repetidores para guardar las pulsaciones de teclas y realizar acciones más rápido. Escribe **`n`** para repetir una búsqueda. Escribe **`.`** para repetir el último cambio. Utilizando una combinación de ambos **`n`** y **`.`** se puede aplicar el mismo cambio en cada búsqueda con solo dos pulsaciones de teclas. Dos pulsaciones de teclas. Eso es rápido.

**Pero, ¿y si te digo que hay una manera más rápida?**

Antes de entrar en eso, ilustremos el combo **`n`** y **`.`** con un ejemplo. Eso nos dará algunos antecedentes nuevos sobre lo que estamos tratando de lograr y nos permitirá destacar cómo el nuevo enfoque mejora en este caso.

Por ejemplo, digamos que estamos en un mercado para destruir pepinos. Somos cazadores de pepinos mortales y robustos, y hay algunos pepinos que necesitan borrarse:

```text
pepino zanahoria lechuga
repollo zanahoria lechuga pepino
pepino pepino zanahoria
col pepino col
```

Una forma de hacerlo sería:

1. Ubica pepino con `/pepino`
2. Destruye pepino con **`daw`**
3. Escribe **`n`** para ir al siguiente objetivo
4. Termina repitiendo el último cambio con el comando **`.`**
5. Repite desde el paso `3` hasta que todos los pepinos se hayan terminado
6. Recoger la recompensa

Resulta que hay una forma aún más efectiva de realizar operaciones en las coincidencias de búsqueda: **`gn`** y **`gN`**. Puedes ver estos dos movimientos como versiones sobrealimentadas de **`n`** y **`N`**.

**`gn`** funciona de la siguiente manera:

1. Si estás encima de una coincidencia de búsqueda, selecciona la coincidencia en *modo Visual*.
2. Si estás en *modo Visual*, extiende tu selección actual hasta el final de la próxima coincidencia.
3. (y la mejor parte) Si estás en modo de *operador pendiente*, **funciona con la próxima coincidencia** .

¿Qué significa todo esto? **Significa que al aprovechar `gn` podemos operar con la próxima ocurrencia con solo presionar una tecla**. Con **`gn`** el comando **`.`** encapsula el significado de **"aplicar este cambio a la próxima ocurrencia"**.

En la práctica, si seguimos el mismo ejemplo anterior usando el comando **`gn`**, seremos mucho más eficientes a la hora de terminar con los pepinos:

1. Buscar pepinos con `/pepino`
2. Aplicar el cambio a la próxima ocurrencia **`dgn`**
3. Repetir el cambio en la próxima ocurrencia **`.`**
4. Solo presiona **`.`** hasta que hayas terminado
5. Recoge las recompensas mucho más rápido

Después de usar **`gn`** no hay necesidad de combinar **`n`** y **`.`** porque **`.`** ya incluye la próxima ocurrencia. **¡Increíble!**.