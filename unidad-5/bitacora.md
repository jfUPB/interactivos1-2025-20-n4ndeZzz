
# Evidencias de la unidad 5

## Actividad 3

# Análisis Comparativo: Comunicación Serial v1 vs v2

## ¿Por Qué Ya No Se Necesita un Delimitador?

La principal diferencia es el cambio de un método de comunicación **basado en texto** a uno **binario**.

* **Método Anterior (Texto):** Los mensajes eran cadenas de texto como `"-52,112,True,False"`, cuya longitud variaba. El salto de línea (`\n`) era un **delimitador** esencial para que el receptor supiera dónde terminaba un paquete de datos completo. Era como usar un punto para finalizar una oración.

* **Método Nuevo (Binario):** Ahora, cada paquete de datos tiene un **tamaño fijo y predecible** de 6 bytes. El receptor ya no busca una señal de "fin", sino que simplemente lee un bloque de 6 bytes. Como el tamaño es constante, el delimitador es innecesario.

---

## Comparación del Código de Recepción

El cambio se refleja directamente en cómo p5.js lee y procesa los datos.

### "CODIGO A" (Basado en Texto)

Se leen datos hasta encontrar un delimitador, se trata como texto y se parsea para extraer los valores.

```javascript
// Espera una cadena de texto terminada en '\n'
let data = port.readUntil("\n"); 
if (data) {
    data = data.trim();
    let values = data.split(","); // Divide la cadena
    if (values.length == 4) {
        // Convierte cada trozo de texto a número o booleano
        microBitX = int(values[0]) + windowWidth / 2;
        microBitY = int(values[1]) + windowHeight / 2;
        microBitAState = values[2].toLowerCase() === "true";
        microBitBState = values[3].toLowerCase() === "true";
    }
}
```

### Código Nuevo (Basado en Bytes)

Se lee un número fijo de bytes y se interpretan directamente sus valores numéricos sin necesidad de parsear texto, lo cual es mucho más eficiente.

```javascript
// Espera a tener exactamente 6 bytes
if (port.availableBytes() >= 6) {
    let data = port.readBytes(6);
    if (data) {
        const buffer = new Uint8Array(data).buffer;
        const view = new DataView(buffer);
        // Interpreta los bytes en posiciones específicas como números
        microBitX = view.getInt16(0); // Bytes 0-1
        microBitY = view.getInt16(2); // Bytes 2-3
        microBitAState = view.getUint8(4) === 1; // Byte 4
        microBitBState = view.getUint8(5) === 1; // Byte 5
    }
}
```

Error ejecutado en el experimento 1:
<img width="969" height="680" alt="image" src="https://github.com/user-attachments/assets/9c8fa502-7f9f-4800-a6ff-40fb561622a8" />

Error ejecutado en el experimento 2:
<img width="951" height="585" alt="image" src="https://github.com/user-attachments/assets/0a93c7ed-4479-447a-9c7e-cdbe4e78fb4e" />

En estos primeros dos casos es importante recalcar que mi erro no fue solo el código, sino que no subí las imágenes correspondientes, al subirlas el resultado fue el siguiente:
<img width="1865" height="874" alt="image" src="https://github.com/user-attachments/assets/70586939-ea9d-4782-92e0-dae3c768f9cf" />

Una vez siendo funcional el código lo que sucede visualmente es que se genera el visual en un loop infinito.


En el último intento, se corrigieron los errores y el visual obtenido es el siguiente:
<img width="1919" height="919" alt="image" src="https://github.com/user-attachments/assets/e6f94f1e-a50e-4558-9b1a-c7bf5f1815a9" />






