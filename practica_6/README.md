# Práctica 6: Marker Visual Localization

Práctica realizada por Jose Luis Laria Urbina

## 1. Organización del código

Lo primero que hice fue ver la documentación que nos da unibotics y ver los códigos que se nos proporcionan, una vez copiados y entendidos empezamos a hacer el código.

## 2. Implementación

Primero definí constantes del entorno como el *tag_size* y coger los tamaños de la imagen, ahora hice un código para que el robot avancase cuando se detectaba un tag.

Una vez realizadas estas "pruebas", me metí con la resolución de solvePnP, la cual me dió muchos problemas, pero al final conseguí sacarla y obtener la posición del tag respecto a la cámara. Ahora calculamos la pósicion respecto al mapa del robot, para esto cree una función que crea la matriz *world_tag* y la multiplico por la matriz inverda de *cam_tag*, la cual es obtenida con el solvePnP.

Una vez que tenemos el problema de la localización visual resulta, añadimos la autolocalización con odometría. A esta tampoco le he dado mucha importancia, porque le robot cuando no detecte un tag, unicamente va a girar en el sitio para encontrar otro, y el yaw se va a ajustar una vez encontrado el nuevo tag. 


## 3. Problemas enfrentados

Hetenido tres grandes problemas:

El primero con solvePnP, no entendía muy bien que parámetros me pedía y que me devolvía, asi que me metí en la documentación y le pedí a la IA que me diera ejemplos de como funcionaba y que me devolvía.

Luego al realizar el cálculo de pasar los resultados del solvePnP a las posiciones del robot, al hacer la multiplicación de las matrices las hacía mal porque los ejes de la cámara están desplazados, y no me daban bien las posiciones del robot.

Y el problema que más he tardado y el provocante de que entregase la práctica tarde, al principio para hacer pruebas puse un tamaño fijo al *focal_length*, lo cual me generaba muchisimos errores, sobre todo lo que ocurria es que después de usar la odometría al girar y detectar un nuevo tag, la posición estimada se empezaba a teletransportar, aunque finalmente se conseguía localizar.

Otros problemas menores han sido que al girar el robot con odometría he tenido que meter un "factor suavizante" porque no se movían al mismo tiempo, o que he tenido que grabar con el móvil, porque al grabar con el portatil

## 4. Video

Dejo un video demostración para ver el funcionamiento del robot:
[![Watch the video]](https://youtu.be/UG14yfcCW-4)