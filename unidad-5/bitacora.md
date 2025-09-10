
# Evidencias de la unidad 5  

## Actividad #1:  

### 1.1. Describe cómo se están comunicando el micro:bit y el sketch de p5.js.  

-   El **micro:bit** está programado en MicroPython para **enviar datos
    por el puerto serial (UART)** a **115200 baudios**.
-   El **sketch de p5.js** usa la librería `p5.webserial` para abrir ese
    puerto, leer los datos entrantes y procesarlos.
-   La comunicación solo va del micro:bit hacia el
    navegador.

------------------------------------------------------------------------

### 1.2. ¿Qué datos envía el micro:bit? 

El micro:bit manda 4 valores en cada ciclo:

``` python
xValue = accelerometer.get_x()
yValue = accelerometer.get_y()
aState = button_a.is_pressed()
bState = button_b.is_pressed()
data = "{},{},{},{}
".format(xValue, yValue, aState, bState)
uart.write(data)
```

-   `xValue`: Aceleración en el eje X (entre aprox. -1024 y 1024).
-   `yValue`: Aceleración en el eje Y.
-   `aState`: Estado del botón A (`True` o `False`).
-   `bState`: Estado del botón B (`True` o `False`).

------------------------------------------------------------------------

### 2. ¿Cómo es la estructura del protocolo ASCII usado?

-   Es un protocolo basado en texto:
    -   Cada mensaje es una línea en formato CSV (valores separados por
        comas).  
    -   Termina con un salto de línea `\n`.  
    -   En el ejercicio:  

```{=html}
<!-- -->
```
    -300,450,True,False\n

Esto hace que p5.js pueda leer la línea completa y dividirla con
`split(",")`.

------------------------------------------------------------------------

###  3. Muestra y explica la parte del código de p5.js donde lee los datos del micro:bit y los transforma en coordenadas de la pantalla.  

``` javascript
if (port.availableBytes() > 0) {
  let data = port.readUntil("\n");
  if (data) {
    data = data.trim();
    let values = data.split(",");
    if (values.length == 4) {
      microBitX = int(values[0]) + windowWidth / 2;
      microBitY = int(values[1]) + windowHeight / 2;
      microBitAState = values[2].toLowerCase() === "true";
      microBitBState = values[3].toLowerCase() === "true";
      updateButtonStates(microBitAState, microBitBState);
    } else {
      print("No se están recibiendo 4 datos del micro:bit");
    }
  }
}
```

Lo que hace: - `port.readUntil("\n")`: lee una línea completa enviada
por el micro:bit.
- `split(",")`: divide la línea en los 4 valores.
- Convierte los dos primeros (`X`, `Y`) en enteros y los ajusta al
tamaño de la ventana (`+ windowWidth/2`).
- Convierte los últimos (`True`/`False`) en booleanos (`microBitAState`,
`microBitBState`).

De esta manera, los datos del micro:bit se transforman en coordenadas y
estados que p5.js puede usar para dibujar.

------------------------------------------------------------------------

### 4. ¿Cómo se generan los eventos A pressed y B released que se generan en p5.js a partir de los datos que envía el micro:bit?  

``` javascript
function updateButtonStates(newAState, newBState) {
  // Evento de "A pressed"
  if (newAState === true && prevmicroBitAState === false) {
    lineModuleSize = random(50, 160);
    clickPosX = microBitX;
    clickPosY = microBitY;
    print("A pressed");
  }

  // Evento de "B released"
  if (newBState === false && prevmicroBitBState === true) {
    c = color(random(255), random(255), random(255), random(80, 100));
    print("B released");
  }

  prevmicroBitAState = newAState;
  prevmicroBitBState = newBState;
}
```

Lo que pasa: - **A pressed**: se detecta cuando el botón A pasa de
`false → true`.
- **B released**: se detecta cuando el botón B pasa de `true → false`.
- Esto se logra comparando el estado **actual** con el **previo**
(`prevmicroBitAState`, `prevmicroBitBState`).

Así, aunque el micro:bit solo envía "True/False", p5.js los interpreta
como **eventos de interacción**.

------------------------------------------------------------------------

### 5. Capturas de pantalla de los algunos dibujos que hayas hecho con el sketch.

<img width="873" height="745" alt="image" src="https://github.com/user-attachments/assets/88517e0e-ebff-49c0-9116-f2d13e8b9c52" />  
<img width="827" height="708" alt="image" src="https://github.com/user-attachments/assets/7d330114-1a0b-4690-9280-ca5f5f2fe07e" />


