# Unidad 1

## 🤔 Fase: Reflect

### Actividad 7 (Parte1)  

*1. Basándote en los ejemplos que vimos de sistemas físicos interactivos al iniciar el curso, describe las tres características que definen a un sistema físico interactivo.*  

__Input (Entrada):__ Capta datos del entorno físico mediante sensores (como botones o sensores).  
__Proceso:__ Interpreta y analiza los datos recibidos mediante algún tipo de lógica o algoritmo. Por ejemplo en un microcontrolador (como micro:bit).  
__Output (Salida):__ Responde al entorno físico a través de interfaces o piezas visuales o auditivas.  

___________________________________________________________  

*2. Explica el modelo input-process-output de Patrick Hübner usando como ejemplo el sistema que construiste con micro:bit y p5.js en la Actividad 06. ¿Cuál fue el input, cuál fue el proceso y cuál fue el output?*  

__Input:__ Cuando el usuario presiona el botón A o B en el micro:bit, el micro:bit envía una señal (el carácter 'A' o 'B') por el puerto serial a la computadora.  

__Process:__ 
```javascript
if (port.availableBytes() > 0) {
  let dataRx = port.read(1);
  if (dataRx == "A") {
    circleX -= 10; 
  } else if (dataRx == "B") {
    circleX += 10; 
  }
}
```  
Aquí, el programa lee los datos del micro:bit. Si lee una "A", mueve el círculo hacia la izquierda. Si lee una "B", lo mueve a la derecha.  

__Output (Salida):__ El círculo se mueve a la izquierda o a la derecha dependiendo del botón que se presione en el micro:b  
__________________________________________________________

*3.¿Cuál es la función de la línea uart.write('A') en el código del micro:bit y qué función en p5.js se encarga de “escuchar” ese mensaje?*  

Esta línea envía el carácter 'A' desde el micro:bit a la computadora mediante la conexión serial (UART) para comunicar eventos al algo visual o gráfico (p5.js).  

En p5.js:  
```javascript
serial.read();
serial.readLine();
```  
La función que “escucha” los mensajes enviados desde micro:bit es serial.read() o serial.readLine().  
___________________________________________________________

*4. ¿Cuál es la diferencia fundamental entre el arte/diseño tradicional y el arte/diseño generativo?*  

EL __Arte/Diseño Tradicional:__ Se crea de forma manual y estática. El autor tiene control total sobre cada parte de la pieza. El resultado final no cambia a menos que el autor lo haga.  

El __Arte/Diseño Generativo:__ Se crea a través de algoritmos. El diseñador crea un sistema que genera múltiples resultados automáticamente y en vivo, con diferentes outputos o resultados basados en entradas, azar o datos en tiempo real. Es más dinámico y interactivo.
___________________________________________________________

*5. Imagina que quieres que un círculo en p5.js cambie a un color aleatorio cada vez que sacudes el micro:bit. Describe qué tendrías que programar en el micro:bit y qué tendrías que programar en p5.js para lograrlo.*  

__En micro:bit (MicroPython):__  
```py
from microbit import *
import random
import uart

uart.init(baudrate=115200)

while True:
    if accelerometer.was_gesture('shake'):
        uart.write('shake\n')
        sleep(500)
```        
__En p5.js (JavaScript):__  
```js
let serial;
let colorActual;

function setup() {
  createCanvas(400, 400);
  serial = new p5.SerialPort();
  serial.open('/dev/tty.usbmodemXXX'); // cambia esto por el puerto correcto
  serial.on('data', recibirDato);
  colorActual = color(255);
}

function draw() {
  background(colorActual);
  ellipse(width/2, height/2, 100);
}

function recibirDato() {
  let dato = serial.readLine().trim();
  if (dato === 'shake') {
    colorActual = color(random(255), random(255), random(255));
  }
}
```
___________________________________________________________  

### Actividad 7 (Parte2)    

__1) ¿Qué fue más desafiante para ti en esta unidad: la parte conceptual (entender qué es un sistema físico interactivo) o la parte técnica (hacer que el micro:bit y p5.js se comunicaran)? ¿Por qué?__    
R/ Creo que la parte "tecnica de lo conceptual" ya que entendía parte del código, pero no completo, por esto digo que entendía lo principal pero no línea a línea, ya que habían código nuevos que jamas habia usado como el de UART.  

__2)Describe el momento “¡Aha!” que tuviste cuando lograste que una acción en el micro:bit (presionar un botón, sacudirlo) tuviera un efecto visible en el canvas de p5.js por primera vez. ¿Qué fue lo que entendiste en ese instante?__    
R/Cuando estaba haciendo el ejercicio 06. solamente me funcionaba el movimiento a la izquierda en el microb, pero me di cuenta que tenía un problema en el código de micro:bit, por lo que tuve leer el código detenidamente y añadir la línea:  
```py
    if button_b.is_pressed():
```

__3) Al inicio de la unidad te pregunté: “¿Este curso para qué me sirve?”. Después de experimentar y construir tu primer prototipo, ¿Cómo ha cambiado o se ha vuelto más concreta tu respuesta a esa pregunta?__    
R/Para mi, directamente para las experiencias interactivas, aunque todas las ramas pueden aprender algo, creo la verdad que es el primer acercamiento a experiencias interactivas.  


__4) El tutorial de la Actividad 05 te llevó paso a paso. ¿Cómo te sentiste con ese método de aprendizaje? ¿Te dio seguridad o preferirías haberlo intentado por tu cuenta desde el principio?__    
R/Me gustó bastante la verdad, no cambiaría nada, principalmente por el hecho de que lo vimos, luego lo hicimos y al final la siguiente actividad consistea en un ejercicio autónomo del cual nos podíamos basar del anterior.


### Actividad 8:  

__Lo que hizo mi compañera diferente:__  
- Organizó mejor los valores configurables:  
Definió una variable moveStep para controlar cuánto se mueve el círculo con cada pulsación (moveStep = 10;). Eso hace que si luego se quiere cambiar la velocidad del movimiento, solo se necesita modificar ese valor en un lugar. Yo puse el 10 directamente dentro de los condicionales, lo que es menos limpio y reutilizable.  

- Agregó una restricción de movimiento:  
Incluyó una línea que evita que el círculo se salga del canvas:  
```js
circleX = constrain(circleX, 25, width - 25);
```

Esto me pareció muy útil. Yo no había pensado en poner límites al movimiento, así que si mantenía presionado un botón, el círculo podía irse fuera de la pantalla.  

- Usó fill("pink") antes de dibujar el círculo:  
Eso le da un color más visible o estilizado al círculo. Yo no cambié el color, así que siempre se muestra en el color predeterminado.

___________________________________________________________  

__Lo que yo hice:__  
- Mi código también funciona, pero es más directo y con menos detalles visuales o de control. No usé una variable para el paso del movimiento, ni me aseguré de que el círculo se mantuviera dentro del lienzo. además, no incluí ningún color personalizado para el círculo, ni una lógica que hiciera más claro el estado de conexión visualmente (aunque sí hay diferente texto del botón). Es decir, resolví el problema básico, pero ella le dió una solución más estructurada y robusta.
  
___________________________________________________________  

__Lo que aprendí de su solución:__  
- Aprendí que es mejor separar los valores como el tamaño del paso en una variable (moveStep), porque facilita hacer cambios o experimentar con distintas velocidades.  
- También entendí la importancia de restringir el movimiento con constrain() para mejorar la experiencia visual y evitar errores.  
- Y que detalles como el color o la posición precisa del botón también hacen que el proyecto luzca más pulido.  
  
___________________________________________________________  

### Actividad 9:  

__Continuar: ¿Qué actividad, video o ejemplo de esta unidad te resultó más inspirador o te ayudó más a entender el potencial de los sistemas físicos interactivos?__  
R//El video del proyecto de los chicos de upb donde había una persona bailando con sensores y según el baile y la conción reproducida en ableton, se generaba un producto visual.  

__Dejar de hacer: ¿Hubo alguna parte que te pareció demasiado abstracta, muy rápida o confusa? ¿Hay algo que crees que podríamos cambiar para que sea más claro?__  
R//Por ahora no, todo bastante claro.  

__Empezar a hacer: ¿Qué te genera más curiosidad ahora? ¿Te gustaría explorar más sensores del micro:bit (luz, temperatura), crear visualizaciones más complejas en p5.js o ver más ejemplos de proyectos artísticos?__  
R//Por ahora lo que mas me ha llamado la atención es la parte del arte generativo.  

__Balance inspiración vs. técnica: ¿Cómo sentiste el equilibrio entre ver los videos inspiradores de la Actividad 01 y la parte técnica de conectar las herramientas en las actividades 03-06?__  
R//Bastante bien pero me hubiese gustado mas ver proyectos mas similares los que ibamos a trabajar en la uynidad 1.  

__Comentario adicional: ¿Hay algo más que quieras compartir sobre tu experiencia en esta unidad introductoria?__  
R//Fue un poco complejo hata cierto punto entender las conexione sy relaciones como input, proceso y outputs, pero todo muy claro luego de practicar.  

  
