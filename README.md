# practica3

Developed with Unreal Engine 4

More info in the Wiki

----
nog vragen: 
- hoe moet het menu eruit zien zoals de omgeving? 
- is hud goed hoe hij is (wss enkel timer tonen als hij potion heeft genomen)
- wat is kwaliteit bij optie configuratie

# Proceso de desarrollo
 
**Fri 29 Oct - feature: add initial menu, play and exit options**: Cuando el jugador abre el juego, ve un menu inicial con las opciones para jugar, configurar, o salir. En este commit solo implementé la opcion para jugar y salir.

**Fri 29 Oct - feature: pause menu**: El menu de pausa es igual al menu inicial. Solo el boton de "jugar" cambiara a "seguir jugando" y habra un texto diciendo que el juego esta pausado.
, 
**Sun 31 Oct - feature: add start of configuration menu**: He empezado con el menu de configuracion, que en este commit solo tiene la opcion de cambiar la resolucion (hay 4 opciones).

**Sun 31 Oct - feature: add end menu**: Cuando el jugador obtiene el oro, el juego se acaba y el jugador puede ver un menu que le da la opcion de salir, o jugar otra vez.

**Wed 3 Nov - feature: add timer, start landscape**: Este es el empiezo del HUD, en donde el jugador puede ver cuanto tiempo le queda de una habilidad. Por eso, tuve que cambiar el codigo del jugador cuando toca una pocima. En la practica 1, lo hice con un delay. Pero ahora necesito algo que puede actualizar el tiempo que le queda al jugador. Por eso, uso un Timer de UE4, que cada x segundos va actualizando un percentaje, que se necesita para el progress bar. En este commit también empezé a jugar un poco con el landscape y los textures.

**Thu 4 Nov - feature: automatic landscape**:

----

# Las pruebas

Las pruebas son iguales a las pruebas en la primera practica.

![](https://user-images.githubusercontent.com/56410697/135642953-e3530de3-d957-4fac-ab29-46ec99c83202.png)

## Prueba 1: cruzar el foso
El jugador tiene que saltar mediante saltos sobre troncos. Se muere cuando toca el agua, y regresa al principio.

## Prueba 2: Escalar la muralla
Aquí, el jugador debe escalar la muralla mientras hay rocas cayendo. Solo caen rocas en el primer y tercer saliente. Cuando el jugador toca una roca, o una roca cae encima del jugador, se muere y regresara al primer checkpoint, que se encuentra después de haber cruzado el foso.

## Prueba 3: Obstáculos móviles
Para avanzar a la segunda prueba, el jugador debe caminar entre obstáculos que se están moviendo, tocar un obstáculo mandara el jugador al segundo checkpoint, después de la prueba 2.

## Prueba 4: Saltar
Después de acabar la tercera prueba, el jugador tendrá que tomar una pócima roja que le hace capaz de saltar más alto, así puede superar esta prueba. Al fin hay un tercer checkpoint.

## Prueba 5: Trampa de cuerdas
En el castillo se encuentra una trampa con cuerdas, si el jugador pisa la cuerda, se muere y se va al último checkpoint.

## Prueba 6: Laberinto
Como ultima prueba, el jugador tendrá que encontrar el lingote dorado para ganar. Tiene que encontrarlo en menos de 22 segundos, por eso debería toma una pócima amarilla para correr más rápido. Si no encuentra el lingote a tiempo, el jugador tiene que empezar de nuevo desde el principio del laberinto.
**Solución:** Segunda puerta, el pasillo a la derecha, segunda puerta, izquierda, derecha

## El fin
Cuando el jugador llega a tocar el lingote dorado, ha ganado y se acaba el juego.



