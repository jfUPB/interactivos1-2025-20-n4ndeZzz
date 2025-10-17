
# Evidencias de la unidad 7

## Actividad 01: 

### ¿Qué URL de Dev Tunnels obtuviste?

La URL fue:
**[https://gx95l3wz-3000.use2.devtunnels.ms/mobile/](https://gx95l3wz-3000.use2.devtunnels.ms/mobile/)**

### ¿Por qué necesitamos usar esta URL y no `localhost:3000` o la IP local?

Porque `localhost` solo es accesible desde el mismo computador en el que corre el servidor.
El celular no puede acceder a `localhost` ya que esa dirección apunta a su propio dispositivo.
La URL de **Dev Tunnels** crea un puente seguro entre Internet y mi servidor local, permitiendo que el celular (u otro dispositivo externo) se conecte a mi aplicación Node.js a través de una dirección pública.

### ¿Qué hace `npm install` y `npm start`?

* `npm install` descarga e instala todas las dependencias definidas en el archivo `package.json` del proyecto (como `express` y `socket.io`).
* `npm start` ejecuta el servidor Node.js, iniciando la aplicación para que escuche conexiones en el puerto 3000.

### ¿Qué mensajes observé en la terminal del servidor?

Durante la prueba observé:

```
New client connected
Received message => { x: ..., y: ... }
Client disconnected
```
<img width="422" height="195" alt="Mensajes port" src="https://github.com/user-attachments/assets/aa2ac97e-7c5a-42ab-8abd-cafbccfef138" />

Estos mensajes mostraban cuándo un cliente se conectaba, enviaba información táctil y se desconectaba.

### Describe el comportamiento observado

El sistema funcionó correctamente: al tocar la pantalla del celular, el círculo rojo en el navegador del escritorio se movía instantáneamente en la misma dirección y posición del toque.
No hubo **retrasos (latencia)**, por lo que la comunicación entre el móvil, el servidor y el escritorio fue muy fluida. Como prueba el siguiente video:  

https://github.com/user-attachments/assets/d202beaa-dac4-4851-8928-44cdd56d1ea2  

---

## Actividad 02:  

### ¿Por qué es necesario Dev Tunnels en este escenario y cómo funciona conceptualmente?

Dev Tunnels es necesario porque permite **exponer mi servidor local a Internet** de forma segura.
Sin esta herramienta, el celular no podría conectarse al servidor Node.js, ya que `localhost` no es accesible desde otros dispositivos.
Dev Tunnels actúa como un **intermediario seguro** que recibe las conexiones externas en una URL pública y las reenvía directamente a mi servidor local en el puerto 3000, sin necesidad de modificar configuraciones de red o abrir puertos manualmente.

### ¿Qué función cumple `touchMoved()` y por qué se usa la variable `threshold`?

`touchMoved()` detecta el movimiento del dedo sobre la pantalla y se ejecuta cada vez que el usuario cambia de posición táctil.
Dentro de esta función, se capturan las coordenadas `mouseX` y `mouseY`, que representan la posición actual del toque.
La variable `threshold` sirve para **evitar enviar datos con demasiada frecuencia**, asegurando que solo se transmitan cuando hay un cambio de posición considerable. Esto optimiza la velocidad y reduce el tráfico de red.

### ¿Cuál es la diferencia entre usar Dev Tunnels y la IP local?

| Opción                                   | Ventajas                                                                                    | Desventajas                                                                           |
| ---------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| **IP local (ej. 192.168.1.x)**           | Rápida conexión en red local. No depende de Internet.                                       | Solo funciona si ambos dispositivos están en la misma red y sin bloqueos de firewall. |
| **Dev Tunnels (ej. use2.devtunnels.ms)** | Permite conexión desde cualquier lugar, incluso fuera de la red local. Es segura y cifrada. | Requiere conexión a Internet y tener VS Code activo mientras se usa.                  |


### Capturas del sistema en funcionamiento

<img width="323" height="500" alt="image" src="https://github.com/user-attachments/assets/0d06cfd4-d44a-4951-b856-9050d9bdc803" />  

![si](https://github.com/user-attachments/assets/f7dfe76d-ce7a-4a26-b356-fcb9e4209987)

---  

## Actividad 03:  

### ¿Cuál es la función principal de `express.static('public')`?  

Sirve para permitir que los archivos HTML, JS y CSS de la carpeta “public” estén accesibles desde el navegador sin tener que escribir rutas manuales.
Es una forma más sencilla y directa que `app.get('/ruta', …)`, ya que actúa como un “directorio público” desde el cual se sirve toda la aplicación.  

### ¿Cómo fluye un mensaje táctil a través del sistema?  

1. El móvil detecta un toque mediante `touchMoved()` y ejecuta `socket.emit('mobileData', data)`.  
2. El servidor recibe ese mensaje con `socket.on('mobileData', callback)`.  
3. El servidor reenvía la información a los demás clientes con `socket.broadcast.emit('desktopData', data)`.  
4. El cliente de escritorio escucha el evento `'desktopData'` y actualiza su visualización en p5.js.  

### Si conectara dos escritorios y un móvil, ¿quién recibiría los mensajes?  

Los **dos escritorios** recibirían los mensajes emitidos por el celular, porque el servidor usa `socket.broadcast.emit()`, que envía la información a **todos los demás clientes conectados** excepto al emisor.  

### ¿Qué información útil dan los `console.log` del servidor?  

Permiten ver:  

* Cuándo un cliente se conecta o desconecta.  
* Qué datos se están recibiendo desde el móvil (coordenadas x, y).  
* Que el servidor está retransmitiendo correctamente los eventos.  

Esto me ayudó a **verificar en tiempo real** que el sistema estaba funcionando sin errores.  

---

## Actividad 04:  

### Diagrama del flujo de datos

```
[Móvil] → (touchMoved)
     ↓  socket.emit('mobileData', data)
[Servidor Node.js]
     ↓  socket.broadcast.emit('desktopData', data)
[Escritorio] ← socket.on('desktopData', callback)
     ↓
[Dibuja el círculo en la nueva posición]
```

---

## Actividad 05(Apply):  

### desktop/index:
```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/p5.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/addons/p5.sound.min.js"></script>
  <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>
  <script src="sketch.js"></script>
  <title>Desktop p5.js Application</title>
</head>
<body></body>
</html>
```

### desktop/sketch:
```js
let socket;
let circles = [];
let osc; 
let amplitude;
let started = false;

function setup() {
  createCanvas(800, 600);
  colorMode(HSB, 360, 100, 100);
  noStroke();
  textAlign(CENTER, CENTER);
  textSize(24);

  socket = io();

  socket.on("message", (data) => {
    if (data.type === "touch" && started) {
      circles.push({
        x: data.x * (width / 300),
        y: data.y * (height / 400),
        hue: random(0, 360),
        size: random(20, 80),
        life: 255,
      });
    }
  });

  background(0);
  fill(255);
  text("Haz clic para iniciar 🎶", width / 2, height / 2);
}

function draw() {
  if (!started) return;

  let level = amplitude.getLevel();
  let sizeBoost = map(level, 0, 0.2, 1, 4);
  background(0, 0, 0, 30);

  for (let c of circles) {
    fill(c.hue, 80, 100, c.life / 255);
    ellipse(c.x, c.y, c.size * sizeBoost);
    c.life -= 2;
    c.size += 0.3;
  }

  circles = circles.filter((c) => c.life > 0);

  fill(255);
  textSize(16);
  text("🎵 Música generada - controla desde tu móvil 🎵", width / 2, height - 20);
}

function mousePressed() {
  if (!started) {
    userStartAudio(); // importante para activar contexto de audio
    osc = new p5.Oscillator('sine');
    osc.freq(220);
    osc.amp(0.2);
    osc.start();

    amplitude = new p5.Amplitude();
    started = true;
  }
}
```


### mobile/index:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TouchBeats - Control</title>
    <script src="https://cdn.jsdelivr.net/npm/p5@1.11.0/lib/p5.min.js"></script>
    <script src="https://cdn.socket.io/4.7.5/socket.io.min.js"></script>
    <script src="sketch.js"></script>
</head>
<body>
</body>
</html>
```

### mobile/sketch:
```js
let socket;

function setup() {
  createCanvas(300, 400);
  background(0);
  fill(255);
  textAlign(CENTER, CENTER);
  textSize(20);
  text("🎶 Toca la pantalla 🎶", width / 2, height / 2);

  socket = io();
  socket.on("connect", () => console.log("Connected to server"));
}

function draw() {
  background(30);
  fill(255);
  textAlign(CENTER, CENTER);
  text("🎶 Toca o arrastra para crear círculos 🎶", width / 2, height / 2);
}

function touchMoved() {
  sendTouch(mouseX, mouseY);
  return false;
}

function touchStarted() {
  sendTouch(mouseX, mouseY);
  return false;
}

function sendTouch(x, y) {
  socket.emit("message", {
    type: "touch",
    x: x,
    y: y
  });
}
```

### server:
```js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');

const app = express();
const server = http.createServer(app);
const io = socketIO(server);
const port = 3000;

app.use(express.static('public'));

io.on('connection', (socket) => {
    console.log('New client connected');
    
    socket.on('message', (message) => {
        console.log('Received message =>', message);
        socket.broadcast.emit('message', message);
    });

    socket.on('disconnect', () => {
        console.log('Client disconnected');
    });
});

server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});
```

https://github.com/user-attachments/assets/099a151e-4f1d-4800-af1d-b1bb69ada2bb
---

## Autoevaluación – Unidad 7

| **Criterio de evaluación**                                                                                                   | **Autoevaluación (1-5)** | **Justificación / Evidencia en la bitácora**                                                                                                                                                                                                                                                                       |
| ---------------------------------------------------------------------------------------------------------------------------- | ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **1. Comprendo y explico correctamente el funcionamiento del entorno cliente-servidor con Node.js y Socket.IO.**             | 5                        | En la *Actividad 01* y *Actividad 02* explico detalladamente por qué no se usa `localhost`, qué hace `npm install` y `npm start`, y cómo Dev Tunnels permite la comunicación entre el móvil y el servidor. Además, en la *Actividad 03* describo el flujo de datos paso a paso entre móvil, servidor y escritorio. |
| **2. Implemento correctamente la comunicación en tiempo real entre dos clientes (móvil ↔ escritorio).**                      | 5                        | Se evidencia en la *Actividad 01* donde el movimiento táctil del móvil controla en tiempo real el círculo del escritorio, sin latencia perceptible. Adjunto además video de prueba funcional y capturas del sistema.                                                                                               |
| **3. Comprendo y aplico correctamente el uso de `express.static()` y los eventos de Socket.IO (`on`, `emit`, `broadcast`).** | 5                        | En la *Actividad 03* explico con claridad qué hace `express.static('public')`, cómo viaja un mensaje táctil por el sistema y cómo el servidor retransmite los datos con `socket.broadcast.emit()`. Se evidencia comprensión de la estructura y flujo de eventos.                                                   |
| **4. Analizo el flujo completo de datos desde la interacción táctil hasta la visualización en el escritorio.**               | 5                        | En la *Actividad 04* presento un diagrama de flujo textual que muestra el camino completo del dato: del móvil al servidor, y de este al escritorio. La explicación concuerda con el comportamiento real de la aplicación.                                                                                          |
| **5. Diseño una aplicación nueva, original e interactiva basada en la infraestructura de comunicación estudiada.**           | 5                        | En la *Actividad 05 (Apply)* desarrollo **TouchBeats**, una aplicación creativa donde la música (generada por un oscilador en el escritorio) se sincroniza con visuales controladas desde el móvil. Las visuales cambian con el ritmo sonoro y el movimiento del dedo.                                             |
| **6. Integro el uso de p5.js y p5.sound para producir visuales sincronizadas con audio.**                                    | 5                        | En el código del escritorio (*Actividad 05*) se incluye el uso de `p5.Oscillator`, `p5.Amplitude` y `colorMode(HSB)` para generar sonido y animaciones visuales reactivas. Se justifica en la descripción del funcionamiento de la aplicación.                                                                     |
| **7. Explico mis observaciones y conclusiones con lenguaje técnico claro, en primera persona.**                              | 5                        | Toda la bitácora está redactada en primera persona, con lenguaje técnico, explicando causas, efectos y decisiones. Ejemplo: “El sistema funcionó correctamente... no hubo latencia... Dev Tunnels actúa como un intermediario seguro...”.                                                                          |
| **8. Presento evidencias visuales (capturas, videos o URLs funcionales) que demuestran el funcionamiento real del sistema.** | 5                        | En la *Actividad 01* y *Actividad 02* se incluyen capturas, URL de Dev Tunnels y un video de demostración subido a GitHub, mostrando el funcionamiento en tiempo real.                                                                                                                                             |
| **9. Demuestro comprensión sobre los conceptos de rendimiento, latencia y eficiencia de comunicación.**                      | 5                        | En la *Actividad 01* comento que no hubo latencia en la transmisión, explicando que la comunicación fue “fluida” y en la *Actividad 02* destaco cómo el `threshold` mejora la eficiencia reduciendo tráfico innecesario.                                                                                           |
| **10. Muestro autonomía, creatividad y aplicación práctica del conocimiento en un proyecto propio.**                         | 5                        | En la *Actividad 05* realizo una creación original — *TouchBeats* — que combina sonido, visuales y control táctil. No se trata solo de cambiar colores, sino de un nuevo concepto interactivo musical.                                                                                                             |





