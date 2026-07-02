# Práctica 6: Marker Visual Localization

Práctica realizada por Jose Luis Laria Urbina

## 1. Organización del código

Lo primero que hice fue ver la documentación que nos da unibotics y ver los códigos que se nos proporcionan, una vez copiados y entendidos empezamos a hacer el código.

## 2. Implementación

Primero definí constantes del entorno como el *tag_size* y coger los tamaños de la imagen, ahora hice un código para que el robot avancase cuando se detectaba un tag.

Una vez realizadas estas "pruebas", me metí con la resolución de solvePnP, la cual me dió muchos problemas, pero al final conseguí sacarla y obtener la posición del tag respecto a la cámara. Ahora calculamos la pósicion respecto al mapa del robot, para esto cree una función que crea la matriz *world_tag* y la multiplico por la matriz inverda de *cam_tag*, la cual es obtenida con el solvePnP.

Una vez que tenemos el problema de la localización visual resulta, añadimos la autolocalización con odometría. He tenido que hacer cambios en el planteamiento de esta debido al cambio de comportamiento del robot en la nueva actualización, ahora además de girar en el sitio, avanza lentamente, esto la verdad que es bastante problemático porque el robot a la minima que se choca con una pared se queda pillado y se "desliza", lo que provoca que la odometría acumule mucho error y se acabe perdiendo. Una vez encontrado el nuevo tag, la visión recupera el control de la localización.

## 3. Problemas enfrentados

Hetenido tres grandes problemas:

El primero con solvePnP, no entendía muy bien que parámetros me pedía y que me devolvía, asi que me metí en la documentación y le pedí a la IA que me diera ejemplos de como funcionaba y que me devolvía.

Luego al realizar el cálculo de pasar los resultados del solvePnP a las posiciones del robot, al hacer la multiplicación de las matrices las hacía mal porque los ejes de la cámara están desplazados, y no me daban bien las posiciones del robot.

Y el problema que más he tardado y el provocante de que entregase la práctica tarde, al principio para hacer pruebas puse un tamaño fijo al *focal_length*, lo cual me generaba muchisimos errores, sobre todo lo que ocurria es que después de usar la odometría al girar y detectar un nuevo tag, la posición estimada se empezaba a teletransportar, aunque finalmente se conseguía localizar.

Otros problemas menores han sido que al girar el robot con odometría he tenido que meter un "factor suavizante" porque no se movían al mismo tiempo, o que he tenido que grabar con el móvil, porque al grabar con el portatil.

A la hora de hacer bien la odometría, me encontré con que mi código actual en la nueva actualización se comportaba de manera extraña, ya que el comportamiento del choque con las paredes es distinto, por lo que como he comentado he tenido que meter velocidad lineal. También he tenido que meter un "suavizado" a la hora de calcular la posición. Ajustando este parámetro se conseguiría una mejor localozación con odometría. 

## 4. Video

Dejo un video demostración para ver el funcionamiento del robot:
[![Watch the video]](https://www.youtube.com/watch?v=9AqheWXfXD0)