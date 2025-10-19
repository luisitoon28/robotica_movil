# Práctica 2: Siguelineas

Práctica realizada por Jose Luis Laria Urbina

## 1. Organización del código

Para organizar la estructura del código, sabiendo que tenía que tenía que ser implementada con un PID y usando opnecv, he usado como ayuda la práctica_6 de Arquitectura software para robots, en la que se implementa un PID.

Para ello he creado, varias funciones: una devuelve la mascara de color rojo que hay que seguir, otra para calcular los errores lineales y angulares y otras para calcular las velocidades.

## 2. Implementación

Para poder detectar la linea roja, primero he pasado los valores obtenidos por la cámara a HSV, he creado dos rangos de rojo, para poder detectar distintos tonos. Como es obvio no me he quedado con todos los rojos detectados, he cogido una pequeña franja en el centro y dependiendo de lo lejos que está del centro horizontal, calculo el error, haciendo una aproximación de normalizar, y siendo el error lineal, el contrario al angular.

Para el pid, simplemente he ido ajustando los valores de kp, kd y ki, aquí veremos que falta la ki, esto lo comentaré más tarde. Por último al valor obtenido del pid, ya normalizado, lo multiplico por la velocidad máxima y en el caso de la velocidad angular, también tengo una correción para la velocidad mínima y en el caso de la angular lo multiplico por -1, ya que el error hacia la derecha es positivo, pero para girar a la derecha la velocidad a introducir es negativa y viceserva.

Para el "estado" de recuperación, simplemente he hecho que cuando el error sea 0 en ambos, que se ponga a girar, esto en un principio no debería dar errores porque unicamente los dos erroes deberían ser cero cuando no se detecta la linea. En el video del circuito Nurburgrin se puede ver el comportamiento.

## 3. Problemas enfrentados

He tenido varios problemas, algunos en la forma de querer solucionar el problema y otros en el código.

Uno de los primeros problemas que me enfrenté, es que no usé opencv, ya que no sabía que se podía usar, y filtraba la imagen "a lo bruto" cogiendo el color rojo en diferentes franjas.

Otro de los problemas más grandes ha sido como he querido plantearlo, ya que mi solución tiene un pequeño problema, que coje las curvas por el interior en vez de seguir de manera estricta la linea, para solucionar esto, quise hacer dos franjas distintas para cada velocidad. La de la velocidad lineal estaría en el medio de la imagen y la de la angular un poco más abajo, para que antes de coger una curva, el coche frenase y luego girase, además al estar la franja estaría "más cerca" del coche, asi que este iría por el centro casi siempre, pero ha sido imposible hacer esto, ya que me he encontrado varios problemas como ajustar bien las k o las curvas muy cerradas.

Como he comentado en le punto anterior, mi solución no tiene ki, esto se debe a que al principio tenía una ki muy pequeña porque considero que el offset es minimo, pero al terminar una o varias vueltas, el coche empezaba a distanciarse un poco a la derecha de la linea, al quitar la ki este problema desapareció, por lo que decidí eliminarla.

Por último, había ocasiones en las que la ejecución se me detenía de golpe, por un error en la banda, ya que hay en ocasiones que esta no devuelve nada porque no detecta color rojo, asi que hice q si está vacia devuelve ceros.
## 4. Video

Dejo un video demostración x10 de velocidad para ver el funcionamiento del robot en:

Circuito simple, 
[![Watch the video]](https://www.youtube.com/watch?v=GNgtHxaxMD8)

Circuito Nurburgrin, 
[![Watch the video]](https://www.youtube.com/watch?v=SCmjc-E2bA4)
