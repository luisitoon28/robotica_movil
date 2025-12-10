# Práctica 5: Laser Mapping

Práctica realizada por Jose Luis Laria Urbina

## 1. Organización del código

Antes de ponerme a picar código, hice trazas de las posiciones del robot del Odom y del laser, viendo que el laser es de 360º, que su distancia máxima es 3.5 metros, que si no detecta nada a más de 3.5 devuelve inf.

Para los mapas he creado dos arrays:

probability_map -> mapa de probabilidad
draw_map -> dibujar el mapa

Las probabilidades que he usado son 0.2 cuando está libre y 0.8 cuando está ocupado.

Para bayes he calculado la probabilidad fuera del bucle para no calcularlas todas las iteraciones.


Primero al ser todas las probabilidades 0.5 por no haber mapeado nada, el log de dicha probabilidad es 0, por lo que el mapa de probabilidad lo he inicializado a 0 y el draw a 100

## 2. Implementación

Para la creación del mapa, he creado varias funciones.

La primera divide los rayos del laser en 50 puntos, compruebo si ha chocado con algo viendo la distancia que nos da el rayo, ahora cojo cada uno de los 50 puntos y veo su posición en el mapa, le modifico la probilidad de un punto y lo meto en un set, ahora, si el siguiente punto está en el set, no lo modifico, porque si no estaría modificnado la probabilidad de un punto más de una vez por rayo de laser. 

Para asignar la probabiliad de los obstáculos, miro si ha chocado el laser, y si ha chocado el último punto del rayo le suma la probabilidad de obstáculo.

La segunda función es para dibujar el mapa y sumar los valores probabilisticas, le paso el punto a modificar y el valor, lo sumo, limitando us valor a +-20, para que no tarde mucho en revertir una probabilidad y dependiendo del valor probabilístico final de dicha posición le asigno al draw_map occupied o free.

Para las mediciones del laser sean independientes, he hecho que solo se actualicen los mapas cada vez que el robot avanza medio metro.

A la hora del movimiento, he creado una máquina de estados, primero el robot va hacia delante hasta quedarse a 2 metros de la pared y el segundo gira un ángulo determinado, dependiendo de si hay una pared cerca.

El angulo del giro va a depender de si el laser detecta una pared cerca, si la detecta a la izquierda, el robor girará a la derecha.

Para ver si se ha detectado una pared al ir hacia delante, tengo una función para coger una ventana de x grados en la parte frontal y devuelvo el valos más pequeño de dicha ventana y para los laterales tengo una función que coje los valores del laser, descarta los valores no válidos, ahora miro los valores de la mitad a la derecha e izquierda y eligo a cual de los dos ir.


## 3. Problemas enfrentados

Para el movimeinto he intentado hacer un movimiento basado en fronteras, mirando cual es la posicióm más cercana al robot que tiene valores probabilisticos vacíos junto con probabilidades sin calcular, es decir 0, para dirigir con un pid al robot, pero no me ha dado tiempo a terminarlo y he decidido volver al movimiento sistemático.

He tenido que ajustar las posiciones para que estén centradas en la imagen, ya que en un inicio estaban en una esquina.

## 4. Video

Dejo un video demostración para ver el funcionamiento del robot:
[![Watch the video]](https://youtu.be/usREJzRY2_k)

## 5. Comparación de Odom2 y Odom3

Como podemos ver en las imagenes, con Odom2 al tener algo más de ruido el mapa no está bien pero se parece al Odom, pero al meter aún más ruido con el Odom3 el mapa ni se completa.

Odom:
![alt.text]( "Odom")


Odom2:
![alt.text]( "Odom2")


Odom3:
![alt.text]("Odom3")
