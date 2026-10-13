## Metodología

### Medición y control de temperatura

### 1. Montaje del sistema de medición

Para medir la temperatura en la encubadora a escala, se utilizó; un termistor NTC, donde la resistencia disminuye cuando la temperatura aumenta. El sensor se conectó a la ESP32 con un divisor de voltaje por el termistor y una resistencia fija de 3,3 kΩ.

El voltaje del punto medio del divisor se conectó al pin GPIO 34 de la ESP32.

<img width="400" alt="CircuitoTemp" src="https://github.com/user-attachments/assets/fc4ef49a-3601-45e3-8026-ee0e968123e2" />

**Figura 1. Circuito de medición de temperatura con termistor NTC y ESP32.**


### 2. Adquisición y procesamiento de la señal

En Arduino IDE. Para cada ciclo la ESP32 tomó 100 muestras de voltaje y calculó su promedio para reducir las fluctuaciones de la lectura.
A partir de este voltaje promedio, se calculó la resistencia del termistor.

\[
R_{NTC}=R_F\left(\frac{V_{CC}-V_{NTC}}{V_{NTC}}\right)
\]

Donde:

- \(R_{NTC}\): resistencia calculada del termistor.
- \(R_F\): resistencia fija de 3,3 kΩ.
- \(V_{CC}\): voltaje de alimentación de 3,3 V.
- \(V_{NTC}\): voltaje medido en el punto medio del divisor.

La resistencia obtenida se utilizó para estimar la temperatura en grados Celsius, basada en puntos de calibración experimentales.

### 3. Calibración del termistor

La calibración se hizo utilizando mediciones de temperatura de referencia y sus valores de resistencia. Se emplearon puntos de referencia aproximados de 18 °C, 24 °C, 36 °C y 37 °C.
La temperatura calculada se consideró una estimación experimental.

### 4. Implementación del control de temperatura

La temperatura estimada se utilizó como variable de entrada para la lógica de control implementada en la ESP32. El sistema acciona un módulo relé conectado al GPIO 26, que permite controlar el elemento calefactor del prototipo.

El relé funciona con una lógica activa en nivel bajo: una señal `LOW` lo activa y una señal `HIGH` lo desactiva.

La lógica de control se configuró de la siguiente manera:

- **Temperatura inferior a 36 °C:** se solicita calentamiento.
- **Temperatura igual o superior a 37 °C:** se desactiva el calentamiento.
- **Temperatura igual o superior a 37,5 °C:** se mantiene el calentamiento desactivado y se genera una alerta de temperatura alta.


<img width="400" alt="Completotemp" src="https://github.com/user-attachments/assets/ae29806b-d59d-4223-b1cc-946413e70ed3" />

**Figura 2. Montaje físico del sistema de control de temperatura.**


### 5. Indicadores visuales y supervisión

Se utilizaron dos LED para indicar el estado del sistema. El LED verde representa el estado de calentamiento desactivado y una temperatura de 37 °C, y el LED rojo indica una solicitud de calor o indicador de una alta temperatura.


