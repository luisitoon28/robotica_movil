# Práctica 1: aspiradora simple 

Práctica realizada por Jose Luis Laria Urbina

## 1. Organización del código

Para organizar la estructura del código, sabiendo que tenía que tenía que ser implementada con una máquina de estados, he usado la implementacion que nos enseñaron en la asignatura de arquitectura software para robots.

Para ello he creado, tres funciones de movimiento, tres para comprobar si debe producirse un cambio de estado dependiedndo del objetivo del movimeinto, una para realizar el cambio de estado y una para poder normalozar los ángulos.

## 2. Las funciones

1. move_turn(): hace girar el robot un ángulo aleatorio entre *[-90, 90]* grados, esto lo hice calculando el ángulo que había girado y comparandolo con el objetivo marcado, he tenido varias dificultades, pero estas las comentaré en el sigueinte punto.

2. move_reverse(): mueve hacia atás el robot.

3. move_forward(): mueve hacia delante el robot.

4. check_forward_2_reverse(): comprueba el estado del bumper para ver si se tiene que cambiar la dirección del robot.

5. check_reverse_2_turn(): a través de un sistema de ticks, se comprueba si se ha retrocedido la distancia suficiente.

6. check_turn_2_forward(): comprueba si se ha girado ya el ángulo objetivo.

7. go_state(new_state): cambia el estado actual por el estado introducido, ya de paso aprovecho para resetar velocidades y variables globales.

8. normalize_angle(angle): normaliza el angulo recibido por el robot, ya que este viene dado por el rango [0, π] y [-π, 0] y para poder trabajar con ello, necesito que el rango sea de [0, 2π]

## 3. Problemas enfrentados

La función más problemática ha sido la del giro, ya que lo planteé calculando los ángulos de movimiento en vez de por tiempo, lo que me dificultó bastante el movimiento cuando va hacia un "ángulo negativo", aunque luego me di cuenta que la solución era bastante simple, únicamente tenía que restar al ángulo inicial el actual en vez de hacerlo al contrario y luego normalizarlo.

otra función con la que he tenido problemas ha sido con check_reverse_2_turn(), ya que en un principio la habia pensado para que obtuviese la distancia con la pared que se había chocado y que se fuese hacia atrás hasta quedarse a una distancia prudencial, pero, esta aproximacion la dejé de lado porque el sensor al estar muy cerca de una pared obtiene valores erroneos. Al final hice un sistema por ticks.

Por último, el bucle while lo iba a hacer con un switch-case (en Python match-case), pero este me dio problemas y lo decidí cambiar por if-elif.

Por último, dar un punto de vista algo crítico, ya que al ser la práctica en Python he tenido que usar variables globales, lo cual no lo veo del todo correcto, pero al estar acostumbrado a trabajar con clases, estas variables las habría hecho como atributos de la clase.

## 4. Video

Dejo un video demostración x10 de velocidad para ver el funcionamiento del robot.

[![Watch the video]](https://www.youtube.com/watch?v=gbT_UCeMD64)
