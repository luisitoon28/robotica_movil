# Práctica 4: Navegación global

Práctica realizada por Jose Luis Laria Urbina

## 1. Organización del código

Para organizar la estructura del código, sabiendo que tenía que divir el código en varias partes he creado, varias funciones: una para crear el mapa de costes y dibujarlo, otra para agrandar los obstáculos, otra para coger los valores más pequeños en un rango de 4 posiciones y un pid para mover el coche. 

Para crear el array de costes tengo 2 array más de apoyo, uno booleano que pongo la casilla a True si ya tiene un valor asignada y otra para pintar el mapa, que solo llega hasta 255, ya que si no los valores al pintarlos se reinician porque su rango es de (0-255).

### 1.1 Nombres a usar en la explicación

mapa -> mapa obtenido de *WebGUI.getMap('/resources/exercises/global_navigation/images/cityLargenBin.png')*
draw -> array de valores (0-255) para pintar
costes -> array de los valores que el coche tiene que seguir
visited -> array booleano

## 2. Implementación

Para crear el array de costes he seguido la la API de Unibotics, lo que he hecho es crear una cola para los puntos del mapa, al coger el objetivo lo introduzco en la cola, entro en la función *path_planning* miro sus vecinos y si en el mapa no es un obstaculo y no está ocupada visited, dependiendo de si es en diagonal o no le sumo 1,4 o 1 en el array de costes y del dibujo. 
Los bordes los "ensancho", mirando el mapa y si el valor es una pared miro sus vecinos y si estos no son obstáculo les sumo un valor muy grande, mayor a 255, para que si el objetivo está muy lejos no interfiera con los valores a seguir.

He confirmado que se me hacía bien los costes, printenado en un rango de 4 alrededor del coche, viendo que los valores van disminuyendo de la misma forma que aparece en la API de unibotics.

A la hora de la conducción, primero busco el menor valor en un rango de 4, cojo la posicion del mapa de ese valor y creo un vector coche -> valor mínimo, y otro coche -> goal, ahora se los paso al pid, y calculo el error de la distancia y del angulo del coche respecto al valor mínimo y con eso saco las velocidades, por último calculo la distancia de el coche al objetivo y cuando considero que está suficientemente cerca, se detiene.

Por último, para poder crear otro goal y que el coche se mueva, miro las flags para ver si se puede planificar y si se puede, reinicio los arrays y alguna flag y asigno un nuevo goal.

## 3. Problemas enfrentados

He tenido varios problemas.

Primero a la hora de crear el mapa de costes, lo había planteado para que cada vez que se acabasen de meter en la cola los vecinos, se volviese a llamar a la misma función, es decir, intenté usar recursividad, pero no sabía que hay un "límite" en las veces que se puede llamar a una función recursivamente y nunca me hacía el mapa entero.

Para el ensanchado de os bordes, intenté con distintos valores de "expansión" y al final me quedé con 2, ya que con 1 se me quedaba muy pequeño y con más se me empezaba a pintar las calles también.

Las coordenadas no coinciden en el mapa y gazebo por lo que estuve un tiempo comparandolas con el coche a velocidad lineal baja.

A la hora de coger otro objetivo, he tenido que meter varios booleanos para comprobar que se está ejecutando en ese momento, ya que de no ser así, al coger otro objetivo, podía cortar la ejecución en marcha, cambiarme le goal sin cambiar los costes y hacer que el coche nunca se pare o hacer que se comporte de formas no planeadas.

Para la creación del draw, visited y costes de primeras había cogido el array mapa y lo igualaba a 0 o false, pero esto me parecía una forma algo cutre así para cada uno inicialicé un array numpy a 0/false, lo único, que no se muy bien porque de esta forma se hace mucho más lento el mapa.

Por último, a la hora de ajustar el pid, he tenido problemas ya que en ocasiones se me podía quedar bloqueado, con velocidad muy baja o hacer movimientos raros.

## 4. Video

Dejo un video demostración para ver el funcionamiento del robot:
[![Watch the video]](https://youtu.be/dTHuddeDxXs)
