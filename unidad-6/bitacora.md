
# Apply

## Actividad 5:

### Objetivo

El propósito de este proyecto fue desarrollar una aplicación interactiva en tiempo real que permitiera la comunicación entre dos páginas web diferentes a través de un servidor Node.js utilizando **Socket.IO**. La idea central consistió en que **Page1** funcionara como un panel de control con sliders, mientras que **Page2** actuara como un espacio visual en el que se representaran los cambios enviados desde Page1.

### 2. Desarrollo

*2.1. Infraestructura de comunicación*

* Se utilizó **Node.js con Express** para levantar un servidor local.
* Se integró **Socket.IO** como la capa de comunicación en tiempo real.
* Se definieron eventos personalizados (`win1update` y `getdata`) para que los datos enviados desde una página se redistribuyeran a las demás.

*2.2. Page1 – Panel de control*

* Implementé una interfaz con **sliders** que permiten controlar:

  * Los valores de color (R, G, B).
  * El tamaño del círculo.
  * La posición (X, Y) dentro del lienzo de la otra página.
* Cada vez que un slider cambia, la página emite un mensaje con los datos actualizados al servidor.

*2.3. Page2 – Visualización gráfica*

* Creé un lienzo de 800x600 píxeles donde se dibuja un círculo de luz.
* Los parámetros de este círculo (color, tamaño, posición) se actualizan en tiempo real con los datos que llegan desde Page1.
* El resultado es una representación visual inmediata de lo que el usuario controla en la otra página.

*2.4. Servidor*

* El servidor recibe los datos desde Page1 y los retransmite con un evento llamado `getdata`.
* Page2 escucha este evento y actualiza su visualización en tiempo real.
* Se dejó abierta la posibilidad de que Page2 también pueda enviar datos (`win2update`), lo que permitiría una comunicación bidireccional en versiones futuras.

### 3. Conclusiones

Este caso de estudio demostró cómo es posible implementar comunicación en tiempo real de manera sencilla entre dos interfaces web. La estructura lograda tiene varias ventajas:

* **Claridad**: una página emite datos y la otra los visualiza.
* **Escalabilidad**: es posible extender el sistema para que ambas páginas se comuniquen o incluso integrar más clientes.
* **Creatividad aplicada**: la interacción no se limitó a simples mensajes de texto, sino que permitió un control visual dinámico que enriquece la experiencia del usuario.

### 4. Códigos:

server.js:
```js
const express = require('express');
const http = require('http');
const socketIO = require('socket.io');
const path = require('path');

const app = express();
const server = http.createServer(app);
const io = socketIO(server);
const port = 3000;

// Variables para almacenar los datos de cada página
let page1 = { r: 200, g: 200, b: 200, size: 100, x: 400, y: 300 };
let page2 = {};

app.use(express.static(path.join(__dirname, 'views')));

app.get('/page1', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page1.html'));
});

app.get('/page2', (req, res) => {
    res.sendFile(path.join(__dirname, 'views', 'page2.html'));
});

io.on('connection', (socket) => {
    console.log('A user connected - ID:', socket.id);

    // Cuando llega info desde Page1 → reenviarla a todos los demás
    socket.on('win1update', (window1, sendid) => {
        console.log('Received win1update from ID:', socket.id, 'Data:', window1);
        page1 = window1;
        socket.broadcast.emit('getdata', { data: page1, from: 'page1' });
    });

    // Si en el futuro quieres que Page2 también mande info:
    socket.on('win2update', (window2, sendid) => {
        console.log('Received win2update from ID:', socket.id, 'Data:', window2);
        page2 = window2;
        socket.broadcast.emit('getdata', { data: page2, from: 'page2' });
    });

    socket.on('disconnect', () => {
        console.log('User disconnected - ID:', socket.id);
    });
});

// Validación simple (opcional, puedes omitir si no lo necesitas)
function isValidWindowData(data) {
    return data && typeof data === 'object';
}

server.listen(port, () => {
    console.log(`Server is listening on http://localhost:${port}`);
});
```


page1:
```js
let socket;

function setup() {
    noCanvas(); // Page1 no dibuja, solo manda datos
    socket = io();

    // Referencias a los sliders
    const r = select('#r');
    const g = select('#g');
    const b = select('#b');
    const size = select('#size');
    const x = select('#x');
    const y = select('#y');

    // Función para enviar datos cada vez que cambie un slider
    function sendData() {
        const data = {
            r: int(r.value()),
            g: int(g.value()),
            b: int(b.value()),
            size: int(size.value()),
            x: int(x.value()),
            y: int(y.value())
        };
        socket.emit('win1update', data, socket.id);
    }

    // Detectar cambios en sliders
    r.input(sendData);
    g.input(sendData);
    b.input(sendData);
    size.input(sendData);
    x.input(sendData);
    y.input(sendData);

    // Enviar datos iniciales
    sendData();
}
```


page2:
```js
let socket;
let luz = { r: 200, g: 200, b: 200, size: 100, x: 400, y: 300 };

function setup() {
    createCanvas(800, 600);
    socket = io();

    // Recibir datos en tiempo real desde Page1
    socket.on('getdata', (msg) => {
        if (msg.from === 'page1') {
            luz = msg.data; // Actualizar parámetros de la luz
        }
    });
}

function draw() {
    background(20); // Fondo oscuro para resaltar la luz
    noStroke();
    fill(luz.r, luz.g, luz.b, 180);
    ellipse(luz.x, luz.y, luz.size, luz.size);
}
```


https://github.com/user-attachments/assets/9845af1c-7bb7-4a61-b1be-3bf309e529a1

## Rúbrica:
Rúbrica de evaluación del proceso

**5: realicé las 5 actividades completas y la autoevaluación.**
3: realicé 4 actividades completas y la autoevaluación.
2: realicé 3 actividades completas y la autoevaluación.
1: realicé 2 actividades completas y la autoevaluación.
0.5: realicé 1 actividad completa y la autoevaluación.
0: no realicé ninguna actividad o no realicé la autoevaluación.

Propongo esta nota (5) debido a que todas las actividades estan completas, no solo respondiendo las preguntas sino documentando con capturas de pantalla cada parte del proceso, por lo que se evidencia que se realizaron completas las actividades.
