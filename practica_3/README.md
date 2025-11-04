# Práctica 2: Siguelineas con obstaculos

Práctica realizada por Jose Luis Laria Urbina

## 1. Organización del código

Para organizar la estructura del código, sabiendo que tenía que tenía que ser implementada con un PID y usando el laser, he usado el pid de la práctica anterior y el laser he cogido como referencia el laser que intenté usar en la primera práctica pero que luego eliminé, a parte de la documentación proporcionada por unibotics.

Para ello he creado, varias funciones: una devuelve la mascara de color rojo que hay que seguir, otra para calcular los errores lineales y angulares y otras para calcular las velocidades.

## 2. Implementación

Para poder detectar los obstáculos, he usado la función que nos proporciona unibotics para coger las distancias y la orientación a los obstaculos.
Para los vectores, primero he pasado las coordenadas absolutas del coche a relativas respecto al target actual, con la función proporcionada por unibotics, después para al atractivo he cogido dicha distancia para la fuerza y la he normalizado, además si la distancia es muy creca al target, coge uno nuevo. Para la repulsiva, he cogidos las distancias de los laseres y las he dividido entrela distancia total al cuadrado, he hecho esto porque si no lo pongo la cuadrado coge objetos lejanos como repulsivos, al final he dividio las fuerzas entre 100, para hacer una especia de "normalización". Por último, para la total he sumado las fuerzas, dandole un poco más de paso a los giros.

Para el pid, he usado el de la práctica anterior, pasando como error los vectores de fuerza.

Las fuerzas como ya están normalozadas, no he tenido que multiplicarlas por una constante para que salgan a un tamaño razonable.



## 3. Problemas enfrentados

He tenido varios problemas.

Uno de los primeros problemas que me fue al trastear con las posiciones, ya que al estar en globales me daban cosas muy raras, una vez pasadas a reliativas todo perfecto.

Otro problema ha sido ajustando la alpha y beta de la fuerza total, al principio decicidí darle más peso a la fuerza repulsora, esto hace que mi coche se mueva más despacio, pero me aseguro de que no se choque con los obstaculos, pero me ocurría que en determinados obstáculos frenase tanto que casi no avanzaba, así que he dicidido dejar los pesos de las fuerzas a 1.

Para la fuerza repulsiva lo que he hecho es darle más peso a la fuerza y que a la x, para que la fuerza repulsiva sea mayor en los "laterales del coche" y se quede en el centro de la pista, lo que me ha quitado probelmas, pero me ha añadido otros, como los goals que están muy cerca de un obstáculo o tener que añadir velocidades máximas y mínimas.

## 4. Video

Dejo un video demostración para ver el funcionamiento del robot en:

Circuito simple, aproximadamente 2 minutos:
[![Watch the video]](https://www.youtube.com/watch?v=tNzojPxez74)
