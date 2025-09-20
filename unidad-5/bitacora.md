
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

------------------------------------------------------------------------  

## Actividad #2: 

### Resultados experimentos 1 y 2.
<img width="1076" height="453" alt="image" src="https://github.com/user-attachments/assets/00d4232f-7e76-4b35-a336-90dfaef0bff6" />
<img width="1017" height="453" alt="image" src="https://github.com/user-attachments/assets/2c5038cf-704d-4a81-876f-a010cfa9b7fc" />

### Análisis de la comunicación con micro:bit

__¿Por qué se ve este resultado? (Primer experimento con Texto)__

Cuando puse la opción **Texto**, la aplicación intentó interpretar los
bytes binarios como caracteres ASCII. Como los datos enviados no son
letras sino valores binarios, se ven símbolos raros y sin sentido.

__Relación con la línea de código__

``` python
data = struct.pack('>2h2B', xValue, yValue, int(aState), int(bState))
```

Aquí empaqueto dos enteros de 16 bits y dos enteros de 8 bits en
binario. Al mostrar los datos en **HEX**, vi los bytes reales que
corresponden exactamente a esos valores. Eso me confirma que la salida
binaria viene directamente de este `struct.pack`.

__Ventajas y desventajas del binario frente a ASCII__

-   **Ventajas:** es más eficiente, ocupa menos espacio, se transmite
    más rápido y mantiene la precisión de los datos.
-   **Desventajas:** no es legible para humanos, y depurarlo sin
    convertirlo a HEX es complicado.
    
---

### Resultados experimento 3.
<img width="1013" height="400" alt="image" src="https://github.com/user-attachments/assets/e400eda9-a626-41fa-a441-b5ba551c5df8" />

### Análisis de la comunicación con micro:bit

__¿Cuántos bytes se están enviando?__
En cada mensaje se envían **6 bytes**. Esto es porque el formato `>2h2B` son 2 valores `short` (2 bytes cada uno = 4 bytes) y 2 valores tipo `B` (1 byte cada uno = 2 bytes). Total: **6 bytes**.

__Relación con el formato `>2h2B`__
- `>` indica **big endian**.  
- `2h` son dos enteros cortos con signo (xValue, yValue).  
- `2B` son dos enteros de 1 byte (aState, bState).  

El orden de los datos enviados es:
```
[xValue (2B)] [yValue (2B)] [aState (1B)] [bState (1B)]
```

__Significado de los bytes__
Ejemplo:  
```
00 18 00 54 00 00
```
- `00 18` → xValue = 24  
- `00 54` → yValue = 84  
- `00` → aState = 0 (no presionado)  
- `00` → bState = 0 (no presionado)  

Cada mensaje envía acelerómetro (X, Y) + estado de los botones.

__Valores positivos y negativos__
Como `h` es un entero con signo, los negativos se mandan en **complemento a dos**.  
- Ejemplo: -100 → `FF 9C`  
- Ejemplo: -200 → `FF 38`  

Así que si el acelerómetro da negativos, veremos bytes que empiezan con `FF`.

---

### Resultados experimento 4.
<img width="1023" height="451" alt="image" src="https://github.com/user-attachments/assets/2c38e985-03fb-48f5-b427-7e8f0bff2dca" />


### Observaciones sobre Formatos de Datos: Binario vs. ASCII  

__Diferencia Principal__  

Lo primero que me saltó a la vista fue la **legibilidad**.

* **ASCII:** Pude leer los datos directamente: `272,-1060,False,False`. Es texto claro y directo.
* **Binario:** Vi caracteres extraños (``). Me di cuenta de que el monitor serial intentaba mostrar bytes crudos como si fueran texto, lo cual no tiene sentido sin una decodificación adecuada.

__Mi Perspectiva sobre el Formato Binario__

__Ventajas__
* *Eficiencia:* Me parece muy eficiente. Envía los datos en un paquete de bytes mucho más pequeño, lo que ideal para transmisiones rápidas.
* *Rendimiento:* Entiendo que para un microcontrolador es más rápido procesar esto, ya que no tiene que convertir texto a números.

__Desventajas__
* *Ilegibilidad:* Para mí, es imposible depurar o verificar los datos a simple vista. Necesitaría un programa que los interprete.

---

__Mi Perspectiva sobre el Formato ASCII__

__Ventajas__
* *Claridad Total:* Es increíblemente fácil de leer y depurar. Vi los valores del acelerómetro y los botones al instante, sin necesidad de herramientas extra.
* *Simplicidad:* Es universal. Cualquier sistema puede interpretar una cadena de texto sin problemas.

__Desventajas__ 
* *Es más "pesado":* Me di cuenta de que enviar `"272,-1060,False,False"` consume muchos más bytes que su versión binaria. Esto lo hace más lento y menos eficiente.
* *Procesamiento extra:* El dispositivo que recibe los datos tiene que trabajar más para analizar el texto, separar los valores y convertirlos de nuevo a números.
