# Unidad 1

## 🤔 Fase: Reflect

### 1.Basándote en los ejemplos que vimos de sistemas físicos interactivos al iniciar el curso, describe las tres características que definen a un sistema físico interactivo.
- Combina elementos fisicos y digitales y son por decirlo de alguna forma interactivos en tiempo real.
- Utiliza la logica de programación para interpretar por ejemplo sensores o botones mesiande el software.
- Puede captar datos del entorno como temperatura, proximidad, iluminación etc... por medio de hardware para generar una aplicacion o sistema mas inmersivo. 

### 2.Explica el modelo input-process-output de Patrick Hübner usando como ejemplo el sistema que construiste con micro:bit y p5.js en la Actividad 06. ¿Cuál fue el input, cuál fue el proceso y cuál fue el output?

- En la Actividad06 los inputs eran los botones A y B que eran los que se encargaban de enviar la informacion o unos datos al procesamiento.
- El proceso que hacia era validar si la informacion que le llegaba era la tecla A o la tecla B si eran datos "vacios" osea que no habia una condicion de accion para estos datos, cuando los procesaba y se daba cuanta de que si le llego la información de uno de los botones y dependiendo si era el A o el B sumaba o restaba una cantidad a la posición en X.
- El output era desde draw y en la pantalla se dibujaba un circulo que cambiaba de posicion segun la información previamente enviada.


### 3.¿Cuál es la función de la línea uart.write('A') en el código del micro:bit y qué función en p5.js se encarga de “escuchar” ese mensaje?

- la función de la línea uart.write('A') es la encargada de leer si como A al presionar la tecla, la funcion en el p5.js es port que se encargaba de guardar la informacion que se recibia en el puerto luego colocamos unos condicionales para validar si se presionaba A y si algun dato del puerto coincidia con A.

### 4.¿Cuál es la diferencia fundamental entre el arte/diseño tradicional y el arte/diseño generativo?

- El arte/diseño tradicional es generar arte de una manera simple, o mejor dicho sin tanto software o hardware se puede realizar en papel o digitalmente, sin reglas de proceso al momento de realizarlo, en cambio el arte/diseño generativo en mas mostrar lo que siente el artista en vivo por medio de varios dispositivos de entrada, tambien se manejan en empresas para generar diseños no estaticos, pero este si se maneja por un medio de reglas.

### 5.Imagina que quieres que un círculo en p5.js cambie a un color aleatorio cada vez que sacudes el micro:bit. Describe qué tendrías que programar en el micro:bit y qué tendrías que programar en p5.js para lograrlo.
- Lo que haria es que en el programa de micro.bit programaria el acelerometro para al sentir `shake` envie una información o un dato que seria el que lee o procesa en el p5.js en la funcion de draw en esa parte haria un condicional if de si recibe los datos que atribuye el `shake` le hago un fill random a el circulo previamente creado con un rgba base, entonces cuando se hace el `shake`  me genera en el fill con un rgba diferente cada vez que se cargue el programa da un color diferente al circulo  

Parte 2: reflexión sobre tu proceso (Metacognición)

6.¿Qué fue más desafiante para ti en esta unidad: la parte conceptual (entender qué es un sistema físico interactivo) o la parte técnica (hacer que el micro:bit y p5.js se comunicaran)? ¿Por qué?

- Lo más dificil para mi fue la parte conceptual, por que siento que la parte de programas se me da muy bien y entiendo lo que coloco pero teoricamente se me dificulta entender como funcionan en verdad las cosas por detras y cual es el proceso paso a paso de como se corre los inputs y llegan a ser procesados.

7.Describe el momento “¡Aha!” que tuviste cuando lograste que una acción en el micro:bit (presionar un botón, sacudirlo) tuviera un efecto visible en el canvas de p5.js por primera vez. ¿Qué fue lo que entendiste en ese instante?

- Mi momento "¡Aha!" fue cuando nos entregaron el micro.bot por primera vez y programe que cuando el micro.bit se colocara de cabeza se encendiera la pantalla y mostrara una flecha hacia arriba, fue en ese momento en el que supe que se pueden lograr hacer cosas muy bacanas y entretenidas.

8.Al inicio de la unidad te pregunté: “¿Este curso para qué me sirve?”. Después de experimentar y construir tu primer prototipo, ¿Cómo ha cambiado o se ha vuelto más concreta tu respuesta a esa pregunta?

9.El tutorial de la Actividad 05 te llevó paso a paso. ¿Cómo te sentiste con ese método de aprendizaje? ¿Te dio seguridad o preferirías haberlo intentado por tu cuenta desde el principio?
