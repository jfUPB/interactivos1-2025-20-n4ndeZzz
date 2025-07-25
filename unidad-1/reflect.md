# Unidad 1

## 🤔 Fase: Reflect

## Actividad 7  

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

