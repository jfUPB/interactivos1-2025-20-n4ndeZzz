
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

---

# Evaluación de Bitácora

A continuación se presenta la evaluación del trabajo documentado en la bitácora, basada en la rúbrica proporcionada.

| Criterio | Evaluación y Justificación |
| :--- | :--- |
| **1. Profundidad de la Indagación** | **Nota Obtenida: 4.8 / 5.0 (Excelente)** <br><br> **Justificación:** La bitácora demuestra una curiosidad que va más allá de la implementación. Se investiga la causa raíz de los problemas y se exploran las implicaciones del diseño del protocolo, cumpliendo con el nivel más alto de la rúbrica. <br><br> **Evidencia Clave:** <br> > *Se plantea y responde la pregunta: "¿Por qué se ve este resultado? (Primer experimento con Texto)", demostrando una indagación sobre la causa del error y no solo su observación.* <br><br> > *Se analiza el trade-off entre protocolos en la sección "Mi Perspectiva", abordando la pregunta implícita de "¿en qué escenarios un protocolo es preferible a otro?".* |
| **2. Calidad de la Experimentación** | **Nota Obtenida: 4.7 / 5.0 (Excelente)** <br><br> **Justificación:** Se diseñaron y ejecutaron experimentos precisos para verificar hipótesis y demostrar sutilezas de la comunicación binaria, como la representación de datos negativos. <br><br> **Evidencia Clave:** <br> > *Se utilizó deliberadamente el monitor serial en modo **Texto vs. HEX** para aislar y confirmar la naturaleza binaria de los datos.* <br><br> > *Se realizó una prueba precisa al decodificar manualmente un paquete de bytes (`00 18 00 54 00 00`) y al verificar la representación en **complemento a dos** de los valores negativos (`-100 → FF 9C`).* |
| **3. Análisis y Reflexión** | **Nota Obtenida: 4.9 / 5.0 (Excelente)** <br><br> **Justificación:** Se demuestra una reflexión profunda que conecta claramente la evidencia (capturas, logs) con la teoría. Se construye un modelo mental robusto del flujo de datos y se analiza el *trade-off* entre eficiencia y complejidad. <br><br> **Evidencia Clave:** <br> > *La bitácora articula claramente la relación causa-efecto: "Como los datos enviados no son letras sino valores binarios, se ven símbolos raros".* <br><br> > *Las secciones "Ventajas y desventajas" y "Mi Perspectiva" son una reflexión directa sobre el **trade-off** entre la eficiencia del protocolo binario y la legibilidad/simplicidad del protocolo ASCII.* |
| **4. Apropiación y Articulación de Conceptos**| **Nota Obtenida: 5.0 / 5.0 (Excelente)** <br><br> **Justificación:** Se demuestra una maestría conceptual al explicar los componentes como un sistema interdependiente. Se articulan los detalles técnicos con total claridad y en palabras propias, evidenciando una comprensión profunda a nivel de bytes. <br><br> **Evidencia Clave:** <br> > *La explicación del formato `>2h2B` es impecable, detallando el significado de cada parte: endianness (`>`), tipo de dato (`h`, `B`) y tamaño.* <br><br> > *Se demuestra la comprensión del sistema completo: desde el empaquetado con `struct.pack` en MicroPython hasta cómo esa estructura de bytes es recibida e interpretada en p5.js.* |




