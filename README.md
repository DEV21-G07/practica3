Enlace al .exe (comprimido): https://drive.google.com/file/d/1YTaR9Hd2ZyQcODYSAC7G2rMviVGHEVyR/view?usp=sharing

# El proyecto

Esta práctica empieza con la primera práctica que hicimos en el curso de "desarrollo de videojuegos". Así que tiene el mismo mundo y las mismas pruebas: el jugador tiene que cruzar el agua saltando sobre troncos, escalar un castillo y al fin encontrar el lingote de oro.

Lo que tenemos que hacer ahora, es añadir algunos menús y hacer que el mundo se ve más real usando las herramientas de landscape y foliage, y usando paquetes que contienen cosas como árboles, etc.

Para los menús, necesitamos un menú inicial en donde el jugador ya puede ver el entorno natural. Ahí el jugador puede elegir de empezar con el juego, ir al menú de configuración o salir. También hay un menú de pausa y un menú final. El juego también necesita un HUD donde el jugador, en este caso, puede ver el tiempo total que ya está jugando, y cuando tiene habilidades mejoradas, cuanto tiempo le queda de utilizarlos.

----

# Proceso

## Preproducción (Oct 29)

#### Planificación

Para empezar tuve que pensar en 2 cosas: los menús y el entorno. Ya que he tenido algún problema con GitHub y usar los paquetes de ue4 (que a veces tienen un tamaño demasiado grande), decidí empezar con los menús.

Después tendría que intentar de agregar el paquete del "spruce forest" al GitHub sin problemas, para que no tendría que volver a usar Google Drive.

Además, después del feedback de la practica 1, hay algunas cosas para mejorar, lo que podemos hacer al fin.

#### Estética
El "spruce forest" tiene dos tipos de árboles: para el verano y para el invierno. Por eso tenía que decidir si me gustaría que el juego se encuentre en el invierno o en el verano/otoño. Elegí el entorno de invierno porque eso le da un poco más de misterio al castillo y las montañas.

## Producción

#### Los menús (Oct 29)

Cuando el jugador abre el juego, ve un menú inicial con las opciones para jugar, configurar, o salir.

El menú de pausa es igual al menú inicial. Solo el botón de "jugar" cambiará a "seguir jugando" y habrá un texto diciendo que el juego está pausado. Para conseguir esto, uso el mismo widget del menú inicial, pero anido "bindings" a los textos que deberían cambiarse o que deberían ser visibles o invisibles.

En el menú de configuración, se necesita cambiar la resolución y el nivel gráfico, he decidido de añadir 2 opciones para el nivel gráfico, siguiendo a este tutorial: https://www.youtube.com/watch?v=uLCNedDnWTY

Cuando el jugador obtiene el oro, el juego se acaba y el jugador puede ver un menú que le da la opción de salir, o jugar otra vez.

#### El HUD - paso 1 (Nov 3)
En el HUD el jugador puede ver cuanto tiempo le queda de una habilidad. Por eso, tuve que cambiar el código del jugador cuando toca una pócima. En la practica 1, lo hice con un delay. Pero ahora necesito algo que puede actualizar el tiempo que le queda al jugador. Por eso, uso un Timer de UE4, que cada x segundos va actualizando un porcentaje, que se necesita para el ProgressBar.

Cambie la repetición (el variable "loop" del Timer) de 1 segundo a menos que 1 segundo para que el ProgressBar va bajándose sin saltos (más fluido), porque así el porcentaje se actualiza en pasos más pequeños.

#### Un entorno natural - landscape (Nov 4)
En la practica 1 ya empece con hacer las montañas con la herramienta de landscape. Pero, no se veían muy realistas y el landscape tenía toda la misma textura.

Para mejorar el landscape, empece a hacer mi propio "Landscape Material", usando el tutorial: https://www.youtube.com/watch?v=yCRzOdo4b68, donde vi como hacer los layers del landscape, y como hacer que se ve más aleatorio. He usado texturas que ya había en el contenido de ue4. Para hacer el "grass layer", he mezclado césped con nieve.

Para darle un poco más de realidad a las montañas y para no tener que hacerlo todo con la mano, hice que solo hay nieve/césped en partes que no tienen demasiada inclinación (como en el mundo real). He usado este tutorial: https://www.youtube.com/watch?v=mP8eHwVEA0o&t=783s. También puse un poco de nieve en las montañas con la mano, porque en algunas partes querría más nieve.

Las montañas aún se veían un poco fluido, no como montañas deberían verse. Con la herramienta "erosion" pude hacer que se ve un poco más realista.

#### Un entorno natural - foliage (Nov 5)
Primero, tuve que añadir el "spruce forest" usando git LFS para ficheros grandes. Después empece a experimentar un poco con la herramienta de foliage, para ver como podría poner árboles en el entorno.

Al entender foliage, empece a poner árboles de invierno donde tiene sentido. Para hacer el "lighting build" salieron algunos errores, para resolverlos tuve que darle un lightmap menos pesado al los árboles del foliage, y hacer que las luces del juego eran dinámicos.

#### Mejorar la practica 1 (Nov 10 y Nov 16)
Con el feedback de la practica 1, me di cuenta de que hay algunas cosas para mejorar.
1. Le di más estructura a los ficheros y los objetos en el nivel.
2. En el código de la pócima, querría que la pócima se desaparece y después de unos segundos se aparece de nuevo. El problema aquí era que también tuve que desactivar los colisiones, porque si no el jugador cuando tocaba la pócima, y se quedó ahí, estaba todo el rato consiguiendo los incrementos. Después de usar ue4 más, me di cuenta de que podía solo hacer que la pócima se destruye, y después de un tiempo ponerlo ("spawn") otra vez en el nivel.
3. Para los bloques de piedra que se mueven, tenía dos clases para uno que empieza a moverse a la derecha, y uno que empieza a la izquierda. Ahora me queda claro que esto es totalmente innecesario, y se puede hacer un objeto y solamente hacer que la dirección inicial es un parámetro.
4. Tuve que añadir más comentarios y más estructurados.
5. En la practica 1 no he personalizado nada, así que ahora personalice un poco más el menú inicial y el castillo.


#### El menú inicial (Nov 12)
Después de implementar el menú inicial, aún había algunas cosas que hacer. Cuando entra el jugador en el juego, ya debería tener una vista del entorno y el castillo. Esto se puede hacer cambiando el offset del cámara que sigua al jugador.

Aquí encontré un problema pequeño, la cámara necesita un poco de tiempo para cambiar su posición, no puede pausar el juego demasiado rápido o el offset no estará anadido. Por eso, necesitaba añadir un delay entre mover la cámara y pausar el juego. Pero con este delay, el jugador tenía un periodo de tiempo donde podía mover el cursor y se cambia la vista. Para resolver esto, al entrar en el juego, le quito inmediatamente el control del cursor al jugador, para que no se mueve la cámara cuando se está poniendo lista para moverse y entrar al menú inicial. Estamos hablando sobre unos milisegundos, no molestaría a un humano.

#### Background y más foliage (Nov 13)
El nivel ya se está viendo muy lindo y muy natural, pero falta ver más allá en el mundo. Además, quería más tipos de foliage con nieve, porque por ahora solo tenía árboles. Empecé a buscar un paquete de ue4 que tiene estas cosas, y que sea gratis. Lo encontré aquí: https://www.unrealengine.com/marketplace/en-US/product/automotive-winter-scene

Pero eran muchos GB, así que quité todo del paquete que no necesitaba, me quedé con los "backgrounds" de montañas y lagos, y con las plantas y los pedazos de nieve. Ya que ya tenía un rio, he puesto el background con un lago grande detrás de eso. Detrás del castillo puse un background de las montañas.

#### HUD elemento permanente (Nov 13)
Ahora ya está todo en el juego, solo necesitaba algo para necesitar realmente el HUD, porque las habilidades mejoradas solo se deberían ver cuando el jugador tiene la habilidad. Para eso, me parecía tener mucho sentido añadir un temporizador en el nivel, para contar cuento tiempo el jugador necesito para llegar al fin. Con eso, el jugador puede intentar de mejorar su tiempo, y hay una parte del HUD que siempre está visible.

----

# Diseño del juego
## Jugabilidad

### Mecánica
**Salud**
- El jugador se muere con un solo golpe o toque de un objeto enemigo.
- Saltando en el agua matará al jugador.
- El jugador se muere si no llega suficiente rápido desde el inicio hasta el fin del laberinto.
- El jugador puede pasar un "checkpoint" para cambiar su ubicación de reaparición.

**Movimientos**
- El jugador puede soltar y maniobrarse para evitar objetos.
- El jugador puede soltar más alto si toma una pócima roja.
- El jugador puede correr más rápido si toma una pócima amarilla.

**Menús**
- Al entrar al juego, el jugador se encuentra en el menú inicial.
- Presionando "esc", el jugador se encuentra en un menú inicial de pausa.
- Ambos menús iniciales tienen las opciones de salir, o irse a un menú de configuración.
- El menú de configuración tiene 3 opciones: cambiar la resolución, la calidad de sombras y la calidad de estructuras.
- Al acabar el juego el jugador ve un menú final, con opciones de jugar otra vez o salir.

### Dinámica
- El jugador necesita evitar o los objetos enemigos para que no se muera.
- El jugador necesita hacer sus movimientos (saltos, …) cuidadosamente para pasarlas pruebas y obstáculos del nivel.
- El jugador tiene que tomar la pócima roja para pasar la prueba de saltos (escalar la muralla hasta llegar adentro).
- El jugador necesita la pócima amarilla para llegar al fin del laberinto suficiente rápido.
- El jugador debería llegar al lingote de oro para acabar con el juego.
- El jugador puede intentar de llegar lo más rápido posible, tiene un temporizador para ver su tiempo.

### Estética
- Ahora es muy importante que el juego se ve muy real, usando landscape, foliage y backgrounds, para que el jugador se siente en un mundo que va más allá.
- Puse neblina y nieve en el entorno para qué se ve un poco más misterioso.
- El temporizador en el HUD debería darle un poco de estrés y sentimiento de prisa al jugador.

## Contenido

### Los enemigos
Los enemigos del jugador son objetos. Hay dos tipos:
- Objetos móviles: Hay rocas en forma de bolas que se caen por la muralla, y después ruedan hacia el agua. El jugador no puede tocarlas o se muere y va al último checkpoint. También hay los cubos de piedras que se mueven de un lado al otro, que pueden matar al jugador y mandarle al último checkpoint.
- Objetos estáticos: Son objetos que no se mueven, pero también pueden matar al jugador, como el agua o las cuerdas adentro del castillo.

Además, hay una prueba especial que matara al jugador si no llega en un tiempo predeterminado. Aquí, el tiempo es el enemigo.

### Los powerups
- Las pócimas rojas: incrementan por unos segundos la altura de saltos del jugador
- Las pócimas amarillas: incrementan por 30 segundos la velocidad del jugador

### Los niveles
Hay un nivel, con varias pruebas, que se puede encontrar aquí: https://github.com/DEV21-G07/practica3/wiki/Las-pruebas
