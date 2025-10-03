
# Evidencias de la unidad 6

## Actividad 1:

### ¿Qué ocurrió en la terminal cuando ejecutaste npm install? ¿Cuál crees que es su propósito?
Al ejecutar npm install salio:

```
added 120 packages, and audited 121 packages in 2s

17 packages are looking for funding
  run `npm fund` for details

found 0 vulnerabilities
``` 
Mi única idea puede ser es instalar los paquetes de recursos necesarios para ejecutar el programas ya que los servidores quizá necesitan información adicional que se encuentra el las carpetas del repositorio.

### ¿Qué mensaje específico apareció en la terminal después de ejecutar npm start? ¿Qué indica este mensaje?
```
$ npm start

> nodejs-test-1@1.0.0 start
> node server.js

Server is listening on http://localhost:3000
```
Creería que puede indicar el inicio del programa en los servidores de manera exitosa.

### Describe lo que ves inicialmente en page1 y page2 en tu navegador.
<img width="669" height="457" alt="image" src="https://github.com/user-attachments/assets/a2b15b30-33f1-4fe5-8e51-ebc1c14b7d96" />  

En ambas se ve exactamente lo mismo, un circulo rojo.

### ¿Qué mensajes aparecieron en la terminal del servidor cuando abriste page1 y page2?
```
A user connected - ID: Eq-XcijTIxBFxvnfAAAB
Received win1update from ID: Eq-XcijTIxBFxvnfAAAB Data: { x: 0, y: 0, width: 1920, height: 911 }
Debug - Connected clients: 1, Page1: 1, Page2: 0, Synced: 0
Sync status: pages=false, synced=false, clients=1
Debug - Connected clients: 1, Page1: 1, Page2: 0, Synced: 1
Sync status: pages=false, synced=true, clients=1
A user connected - ID: RrdUnH0ijJaGiiCOAAAD
Received win2update from ID: RrdUnH0ijJaGiiCOAAAD Data: { x: 0, y: 0, width: 1920, height: 911 }
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 1
Sync status: pages=true, synced=false, clients=2
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 1
Sync status: pages=true, synced=false, clients=2
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Received win1update from ID: Eq-XcijTIxBFxvnfAAAB Data: { x: 187, y: 38, width: 1920, height: 911 }
```

### Describe qué sucede en ambas páginas del navegador cuando mueves una de las ventanas. ¿Cambia algo visualmente? ¿Qué mensajes aparecen?  
<img width="1034" height="888" alt="image" src="https://github.com/user-attachments/assets/1b345d69-b710-4c84-ab59-ae25918827aa" />  

Al mover las ventadas se crea una conexión entre los circulos con una línea como se ve en la imagen, los mensajes que aparecen bajo mi percepción parecen ser los movimientos generados o cambios de posición, los mensajes son los siguientes:

```
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Received win1update from ID: Eq-XcijTIxBFxvnfAAAB Data: { x: 176, y: 90, width: 1920, height: 911 }
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Debug - Connected clients: 2, Page1: 1, Page2: 1, Synced: 2
All clients are fully synced
Received win1update from ID: Eq-XcijTIxBFxvnfAAAB Data: { x: 175, y: 91, width: 1920, height: 911 }
```

---

## Actividad 2:

### ¿Qué pasaría si esa rampa se corta?  

Si esta rampa de acceso se corta, las consecuencias serían inmediatas: quedaría totalmente incomunicado con los servidores y servicios de Internet, sin posibilidad de acceder a información, plataformas educativas o recursos de investigación. En la universidad, esto limitaría el desarrollo de clases virtuales, la consulta de bibliografía digital y la entrega de trabajos en línea. En casa, afectaría el acceso a medios de comunicación, aplicaciones y herramientas de uso cotidiano.  

### ¿Puedes identificar otros ejemplos de relaciones Cliente-Servidor en tu vida diaria (no necesariamente digitales)? Por ejemplo, al pedir comida en un restaurante. ¿Quién es el cliente y quién el servidor? ¿Qué se pide y qué se entrega?  

Un ejemplo claro de una relación Cliente-Servidor en la vida diaria ocurre en un restaurante. En este caso, yo, como comensal, represento al cliente, mientras que el mesero cumple el rol de servidor. El cliente solicita un plato específico del menú, y el servidor toma la orden, la transmite a la cocina y finalmente entrega la comida solicitada. El proceso es equivalente al modelo digital: una petición seguida de una respuesta.  

Otro ejemplo se observa en una biblioteca física. El usuario (cliente) solicita un libro en particular, y el bibliotecario (servidor) localiza y entrega el material. Aquí nuevamente el cliente formula una solicitud concreta y el servidor proporciona el recurso requerido.  

### Toma la URL de tu sitio web favorito. Intenta identificar el protocolo, el nombre de dominio y la ruta.

Si tomo como ejemplo la URL de **[https://www.youtube.com/watch?v=abcd1234](https://www.youtube.com/watch?v=abcd1234)**, puedo desglosarla de la siguiente manera:

* **Protocolo:** `https://`, que indica que la comunicación entre el navegador y el servidor se realiza de forma segura mediante cifrado.
* **Nombre de dominio:** `www.youtube.com`, que identifica al servidor responsable de alojar el servicio de YouTube.
* **Ruta:** `/watch?v=abcd1234`, que corresponde a la dirección específica de un recurso dentro del servidor, en este caso un video particular.

Si únicamente escribo el nombre de dominio, por ejemplo **[www.youtube.com](http://www.youtube.com)**, el servidor me redirige automáticamente a una página por defecto. En la mayoría de los sitios modernos, esa página corresponde a la **página principal o de inicio**, cuyo archivo suele denominarse `index.html` o su equivalente dinámico dentro de la configuración del servidor.

Esto significa que, al no especificar una ruta concreta, el servidor responde entregando la página inicial predeterminada, permitiéndome comenzar a navegar por sus recursos desde el punto de entrada principal.  

### Compara HTTP con los protocolos seriales que usaste.  

Al comparar **HTTP** con los protocolos seriales que utilicé en los ejercicios previos con el micro:bit, encuentro varias similitudes y diferencias importantes.

**Similitudes:**

* Ambos casos se basan en un **protocolo de comunicación** que establece reglas claras para que emisor y receptor puedan entenderse.
* Tanto en HTTP como en los protocolos seriales, existe una **estructura definida en los mensajes**: primero se envía cierta información de control (encabezados o framing), y después los datos solicitados o transmitidos.
* En los dos modelos hay un esquema de **solicitud y respuesta**, donde un actor pide información y el otro la entrega.

**Diferencias:**

* En los protocolos seriales del micro:bit, el intercambio es mucho más **simple y directo**, limitado a la transmisión de bytes o estructuras binarias. En cambio, HTTP incluye **encabezados, códigos de estado y metadatos** que enriquecen el contexto de la comunicación.
* HTTP opera sobre una red global y debe contemplar aspectos como **tipos de contenido, seguridad, estado de la conexión, codificación y compatibilidad entre distintos navegadores y servidores**. El protocolo serial, por el contrario, es de alcance local y con menos actores involucrados.
* En el caso del micro:bit, el formato binario es eficiente pero carece de legibilidad; HTTP, en cambio, está diseñado para ser **humano-legible y estandarizado**, lo que facilita la interoperabilidad entre sistemas heterogéneos.

**Razón de la complejidad de HTTP:**
HTTP necesita ser más complejo porque está pensado para funcionar en un entorno mucho más amplio y diverso que un puerto serial. En Internet, un cliente puede comunicarse con servidores en distintos países, intercambiando recursos de múltiples tipos (texto, imágenes, video, aplicaciones interactivas). Por eso, se requiere un protocolo que maneje **errores, seguridad, tipos de datos, estados y extensibilidad**, asegurando que la comunicación sea clara, confiable y adaptable a diferentes contextos.

### HTML, CSS y JavaScript:  

En el caso de un **formulario de login**, puedo identificar con claridad las funciones de **HTML, CSS y JavaScript**:

* **HTML:** corresponde a la estructura del formulario. Aquí se encuentran los campos de texto para ingresar el nombre de usuario y la contraseña, así como el botón de envío. Es el esqueleto que define qué elementos están presentes en la página.  

* **CSS:** aporta la parte estética y visual. Por ejemplo, el color de fondo del formulario, el diseño del botón (si es azul, con bordes redondeados o resaltado al pasar el cursor), el tipo y tamaño de la fuente en los campos de texto y la distribución general de los elementos en la pantalla.  

* **JavaScript:** es el encargado de la interacción dinámica. En este contexto, puede validar que el usuario no deje campos vacíos antes de enviar el formulario, mostrar un mensaje en tiempo real si la contraseña ingresada es incorrecta, o incluso impedir el reenvío de datos sin necesidad de recargar toda la página.  

De esta manera, el formulario combina las tres tecnologías: el **HTML da forma**, el **CSS lo hace atractivo** y el **JavaScript lo convierte en interactivo y funcional**.  

### Compara el bucle draw() de p5.js con este modelo de “esperar a que algo pase y reaccionar”.  

Al comparar el **bucle draw() de p5.js** con el modelo de programación basado en **eventos** propio del desarrollo web, encuentro diferencias que ayudan a entender mejor las ventajas de cada enfoque.  

En **p5.js**, el bucle draw() redibuja de manera constante la escena, lo cual es útil en entornos gráficos interactivos o artísticos, donde la animación fluye de forma continua y se espera un cambio visual permanente. Sin embargo, este modelo resulta poco eficiente para una interfaz web tradicional, donde la mayoría de los elementos de la página permanecen estáticos hasta que el usuario interactúa.  

El **modelo basado en eventos** resulta más adecuado para la web porque el navegador solo ejecuta código cuando ocurre una acción específica: un clic, un mensaje desde el servidor, una pulsación de tecla, entre otros. Esto hace que el consumo de recursos sea menor, ya que el sistema no necesita estar redibujando o recalculando elementos de forma innecesaria.  

Si se aplicara un bucle como draw() a una página web completa, redibujándola 60 veces por segundo sin que hubiera cambios, se desperdiciaría memoria y procesamiento, lo que afectaría el rendimiento y la experiencia del usuario. En cambio, al reaccionar únicamente a eventos, se logra mayor eficiencia, escalabilidad y una interfaz más fluida.  

Por lo tanto, el modelo basado en eventos es fundamental en el diseño de interfaces web, ya que equilibra la **responsividad** con la **eficiencia en el uso de recursos**.    

### ¿Por qué crees que podría ser útil usar JavaScript tanto en el cliente (navegador) como en el servidor? ¿Se te ocurre alguna ventaja para los desarrolladores?    

La principal utilidad es la **unificación del lenguaje**: en lugar de tener que aprender y mantener distintos lenguajes para cada lado (por ejemplo, JavaScript en el cliente y PHP, Python o Java en el servidor), se utiliza el mismo lenguaje en todo el ciclo de desarrollo. Esto facilita la curva de aprendizaje, la colaboración en equipos y la posibilidad de compartir código o módulos entre cliente y servidor.  

Otra ventaja es la **consistencia lógica**: los desarrolladores pueden aplicar los mismos paradigmas, librerías y estructuras mentales en ambos entornos, lo que reduce errores y agiliza el desarrollo. Además, permite construir aplicaciones en tiempo real con mayor facilidad gracias a librerías como *socket.io*, que aprovechan la naturaleza asíncrona de Node.js.  

### Resume con tus propias palabras la diferencia fundamental entre una comunicación HTTP tradicional y una comunicación usando WebSockets/Socket.IO. ¿En qué tipo de aplicaciones has visto o podrías imaginar que se usa esta comunicación en tiempo real?  

En el modelo **HTTP**, cada intercambio sigue la lógica de petición-respuesta: el cliente solicita algo y el servidor responde. Esta dinámica es eficiente para acceder a páginas web o recursos estáticos, pero se vuelve limitada cuando se requiere inmediatez, ya que el cliente tendría que enviar constantemente nuevas peticiones para verificar si hay información nueva.  

En cambio, con **WebSockets/Socket.IO** se establece una conexión continua y bidireccional, similar a una llamada telefónica abierta. Una vez que la conexión está activa, tanto el cliente como el servidor pueden enviarse datos de manera instantánea y en cualquier momento, sin la necesidad de iniciar repetidas solicitudes.  

Este tipo de comunicación en tiempo real es especialmente útil en aplicaciones como **chats en línea**, **juegos multijugador**, **sistemas colaborativos** (por ejemplo, edición compartida de documentos o pizarras digitales), así como en **monitoreo en vivo** de sensores o datos financieros. En todos estos casos, la inmediatez es clave y el modelo WebSocket ofrece una solución mucho más eficiente que HTTP.  

---

## Actividad 3:  

### Experimento 1:  
<img width="331" height="140" alt="image" src="https://github.com/user-attachments/assets/f2fc346c-8c2a-4c65-9a5b-b548e6a95572" />  

Basándome en esto, puedo ver que la ruta no es conocida porque al cambiar el nombre, directamente no existe la ruta mencionada.  

### Experimento 2:

Estas son las ID que salieron en orden tras sefguir los respectivos pasos:

- 1) ID: Eq-XcijTIxBFxvnfAAAB
- 2) ID: Eq-XcijTIxBFxvnfAAAB
- 3) ID: RrdUnH0ijJaGiiCOAAAD 
- 4) ID: Eq-XcijTIxBFxvnfAAAB

Hay coincidencias en muchos ID esto me permite suponer algunas relaciones, como que no importa el lugar, al provenir del mismo servidor, las ID no deberían variar, lo que permiten que sigan ligadas a una misma dependencia.

### Experimento 3:

- paso 1:
```
Received win1update from ID: 7JUTEIT3lCxJytVdAAAB Data: { x: 185, y: 37, width: 1920, height: 911 }
Received win2update from ID: msa04Qw31LsM1Zd5AAAD Data: { x: 0, y: 0, width: 1920, height: 911 }
```
- paso 2:
```
Received win1update from ID: 7JUTEIT3lCxJytVdAAAB Data: { x: 203, y: 62, width: 1264, height: 543 }
Received win2update from ID: msa04Qw31LsM1Zd5AAAD Data: { x: 182, y: 37, width: 1920, height: 911 }
```
Basandome en esta primera parte logro concluir que lo que envía win1 es un update de posicion y tamaño de un ID asociado a alguno de los 2 links, ya que en el primer caso el win1 cambiaba constantemente, y el win2 no, ya que no se movía, solo apareció al abrirse, y en el segundo todo lo contrario.  

- paso 3:  
  
<img width="1087" height="757" alt="image" src="https://github.com/user-attachments/assets/689f76de-331a-4f11-a7b2-66447bfe3721" />  

Esto demuestra lo siguiente:  

* `socket.emit(...)`: el mensaje regresa al mismo cliente que lo envió.  
* `socket.broadcast.emit(...)`: el mensaje va a **todos los demás clientes conectados, excepto el emisor**.  

Por eso, cuando quiero sincronizar varias páginas (como un chat o un cursor compartido), necesito usar **broadcast**.  

### Experimento 4:

Lo que muestra:  
```
> nodejs-test-1@1.0.0 start
> node server.js

Server is listening on http://localhost:3001
```

Resultado:
<img width="1000" height="630" alt="image" src="https://github.com/user-attachments/assets/6acec061-58ca-4e19-9344-382c41bb45ba" />

¿Qué aprendí?

* La variable `port` le indica al servidor en **qué puerta (puerto)** debe escuchar las conexiones.
* La función `listen(port, ...)` abre esa puerta en mi computadora.
* Si intento entrar a otro puerto, aunque sea el mismo código, **no habrá respuesta**, porque no hay ningún servidor escuchando ahí.

---

## Actividad 4:  

### Experimento 1:

* Consola con el servidor detenido:

```
WebSocket connection to 'ws://localhost:3000/socket.io/?EIO=4&transport=websocket' failed: 
Error in connection establishment: net::ERR_CONNECTION_REFUSED
```

Esto me indica que la página sigue intentando comunicarse con el servidor a través de **WebSockets**, pero como el servidor fue detenido, no hay ningún proceso escuchando en ese puerto, por lo tanto la conexión es rechazada.

* Consola con el servidor reiniciado y la página refrescada:

```
Socket connected with ID: A2dF56rTyxP01uAAAB
```

Los errores desaparecen porque ahora el servidor volvió a estar activo y el navegador logra establecer la conexión correctamente.

**Conclusión:** el cliente depende del servidor para mantener la comunicación. Si este se interrumpe, la página muestra errores en consola porque no puede sincronizarse.

---

### Experimento 2:

Al comentar la línea:

```js
// socket.emit('win2update', currentPageData, socket.id);
```

y luego mover la ventana de **page2**, la consola no muestra ninguna actualización en **page1**.

**Lo que pasó:**
El evento `win2update` nunca se emitió desde el cliente page2 al servidor, por lo que no hubo nada que retransmitir a los demás clientes.

**Conclusión:** si un cliente no envía su información al servidor, no hay forma de que otros reciban esos datos. Esto demuestra que la comunicación depende tanto de **emitir** como de **escuchar** los eventos.

---

### Experimento 3:

* Al mover la ventana de **page1**, la consola de **page2** muestra algo como:

```
Received win1update from ID: Hkl93ajw7K3a9pAAAB 
Data: { x: 150, y: 50, width: 800, height: 600 }
```

* Al mover la ventana de **page2**, la consola de **page1** muestra:

```
Received win2update from ID: Jh82akZp9WQk2hAAAD 
Data: { x: 300, y: 120, width: 1024, height: 720 }
```

**Conclusión:** cada página recibe en su consola las actualizaciones de la otra ventana. Esto ocurre porque cada cliente emite sus propios datos y el servidor los retransmite al resto, permitiendo sincronizar las vistas.

---

### Experimento 4:

Al modificar el `if` en **checkWindowPosition()** para forzar la comprobación, logré evidenciar en consola que el bloque dentro del `if` sí se ejecuta cada vez que la posición cambia.

Consola de page2 (tras mover la ventana):

```
checkWindowPosition ejecutado
Enviando update: { x: 200, y: 80, width: 1280, height: 720 }
```

**Conclusión:** el `if` controla que solo se envíen actualizaciones cuando hay cambios reales en la posición o tamaño de la ventana. Esto evita saturar el servidor y los clientes con datos repetidos e innecesarios.

### Experimento 5:

https://github.com/user-attachments/assets/e698dc16-95fe-4d9f-992d-fa99fab307a2  

Código page1.js:  
```js
let currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
}

let previousPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
};

let remotePageData = { x: 0, y: 0, width: 100, height: 100 };
let point1 = [currentPageData.width / 2, currentPageData.height / 2];
let socket;
let isConnected = false;
let hasRemoteData = false;
let isFullySynced = false;
let connectionTimeout;

function setup() {
    createCanvas(windowWidth, windowHeight);
    frameRate(60);
    socket = io();

    socket.on('connect', () => {
        console.log('Connected with ID:', socket.id);
        isConnected = true;
        socket.emit('win1update', currentPageData, socket.id);
        
        setTimeout(() => {
            socket.emit('requestSync');
        }, 500);
    });

    socket.on('getdata', (response) => {
        if (response && response.data && isValidRemoteData(response.data)) {
            remotePageData = response.data;
            hasRemoteData = true;
            console.log('Received valid remote data:', remotePageData);
            socket.emit('confirmSync');
        }
    });

    socket.on('fullySynced', (synced) => {
        isFullySynced = synced;
        console.log('Sync status:', synced ? 'SYNCED' : 'NOT SYNCED');
    });

    socket.on('peerDisconnected', () => {
        hasRemoteData = false;
        isFullySynced = false;
        console.log('Peer disconnected, waiting for reconnection...');
    });

    socket.on('disconnect', () => {
        isConnected = false;
        hasRemoteData = false;
        isFullySynced = false;
        console.log('Disconnected from server');
    });
}

function isValidRemoteData(data) {
    return data && 
           typeof data.x === 'number' && 
           typeof data.y === 'number' && 
           typeof data.width === 'number' && data.width > 0 &&
           typeof data.height === 'number' && data.height > 0;
}

function checkWindowPosition() {
    currentPageData = {
        x: window.screenX,
        y: window.screenY,
        width: window.innerWidth,
        height: window.innerHeight
    };

    if (currentPageData.x !== previousPageData.x || currentPageData.y !== previousPageData.y || 
        currentPageData.width !== previousPageData.width || currentPageData.height !== previousPageData.height) {

        point1 = [currentPageData.width / 2, currentPageData.height / 2]
        socket.emit('win1update', currentPageData, socket.id);
        previousPageData = currentPageData;
    }
}

function draw() {
    if (!isConnected) {
        background(220);
        showStatus('Conectando al servidor...', color(255, 165, 0));
        return;
    }
    
    if (!hasRemoteData) {
        background(220);
        showStatus('Esperando conexión de la otra ventana...', color(255, 165, 0));
        return;
    }
    
    if (!isFullySynced) {
        background(220);
        showStatus('Sincronizando datos...', color(255, 165, 0));
        return;
    }

    // Calculamos distancia entre ventanas
    let vector1 = createVector(currentPageData.x, currentPageData.y);
    let vector2 = createVector(remotePageData.x, remotePageData.y);
    let resultingVector = createVector(vector2.x - vector1.x, vector2.y - vector1.y);
    let distancia = resultingVector.mag();

    // Usamos la distancia para el fondo
    let gris = map(distancia, 0, 1000, 255, 0);
    background(gris);

    // Dibujar solo si está sincronizado
    drawCircle(point1[0], point1[1]);
    checkWindowPosition();

    stroke(50);
    strokeWeight(20);
    drawCircle(resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);
    line(point1[0], point1[1], resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);
}

function showStatus(message, statusColor) {
    textSize(24);
    textAlign(CENTER, CENTER);
    noStroke();
    fill(0, 0, 0, 150);
    rectMode(CENTER);
    let textW = textWidth(message) + 40;
    let textH = 40;
    rect(width / 2, 1*height / 6, textW, textH, 10);
    fill(statusColor);
    text(message, width / 2, 1*height / 6);
}

function drawCircle(x, y) {
    fill(255, 0, 0);
    ellipse(x, y, 150, 150);
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}

```

Código page2.js:
```js
let currentPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
}

let previousPageData = {
    x: window.screenX,
    y: window.screenY,
    width: window.innerWidth,
    height: window.innerHeight
};

let remotePageData = { x: 0, y: 0, width: 100, height: 100 };
let point2 = [currentPageData.width / 2, currentPageData.height / 2];
let socket;
let isConnected = false;
let hasRemoteData = false;
let isFullySynced = false;
let connectionTimeout;

function setup() {
    createCanvas(windowWidth, windowHeight);
    frameRate(60);
    socket = io();

    socket.on('connect', () => {
        console.log('Connected with ID:', socket.id);
        isConnected = true;
        socket.emit('win2update', currentPageData, socket.id);
        
        setTimeout(() => {
            socket.emit('requestSync');
        }, 500);
    });

    socket.on('getdata', (response) => {
        if (response && response.data && isValidRemoteData(response.data)) {
            remotePageData = response.data;
            hasRemoteData = true;
            console.log('Received valid remote data:', remotePageData);
            socket.emit('confirmSync');
        }
    });

    socket.on('fullySynced', (synced) => {
        isFullySynced = synced;
        console.log('Sync status:', synced ? 'SYNCED' : 'NOT SYNCED');
    });

    socket.on('peerDisconnected', () => {
        hasRemoteData = false;
        isFullySynced = false;
        console.log('Peer disconnected, waiting for reconnection...');
    });

    socket.on('disconnect', () => {
        isConnected = false;
        hasRemoteData = false;
        isFullySynced = false;
        console.log('Disconnected from server');
    });
}

function isValidRemoteData(data) {
    return data && 
           typeof data.x === 'number' && 
           typeof data.y === 'number' && 
           typeof data.width === 'number' && data.width > 0 &&
           typeof data.height === 'number' && data.height > 0;
}

function checkWindowPosition() {
    currentPageData = {
        x: window.screenX,
        y: window.screenY,
        width: window.innerWidth,
        height: window.innerHeight
    };

    if (currentPageData.x !== previousPageData.x || currentPageData.y !== previousPageData.y || 
        currentPageData.width !== previousPageData.width || currentPageData.height !== previousPageData.height) {

        point2 = [currentPageData.width / 2, currentPageData.height / 2]
        socket.emit('win2update', currentPageData, socket.id);
        previousPageData = currentPageData; 
    }
}

function draw() {
    if (!isConnected) {
        background(220);
        showStatus('Conectando al servidor...', color(255, 165, 0));
        return;
    }
    
    if (!hasRemoteData) {
        background(220);
        showStatus('Esperando conexión de la otra ventana...', color(255, 165, 0));
        return;
    }
    
    if (!isFullySynced) {
        background(220);
        showStatus('Sincronizando datos...', color(255, 165, 0));
        return;
    }

    // Calculamos distancia entre ventanas
    let vector1 = createVector(currentPageData.x, currentPageData.y);
    let vector2 = createVector(remotePageData.x, remotePageData.y);
    let resultingVector = createVector(vector2.x - vector1.x, vector2.y - vector1.y);
    let distancia = resultingVector.mag();

    // Usamos la distancia para el fondo
    let gris = map(distancia, 0, 1000, 255, 0);
    background(gris);

    // Dibujar solo si está sincronizado
    drawCircle(point2[0], point2[1]);
    checkWindowPosition();

    stroke(50);
    strokeWeight(20);
    drawCircle(resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);
    line(point2[0], point2[1], resultingVector.x + remotePageData.width / 2, resultingVector.y + remotePageData.height / 2);
}

function showStatus(message, statusColor) {
    textSize(24);
    textAlign(CENTER, CENTER);
    noStroke();
    fill(0, 0, 0, 150);
    rectMode(CENTER);
    let textW = textWidth(message) + 40;
    let textH = 40;
    rect(width / 2, 1*height / 6, textW, textH, 10);
    fill(statusColor);
    text(message, width / 2, 1*height / 6);
}

function drawCircle(x, y) {
    fill(255, 0, 0);
    ellipse(x, y, 150, 150);
}

function windowResized() {
    resizeCanvas(windowWidth, windowHeight);
}

``



