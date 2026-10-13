## Metodología

## Medición y control de temperatura

### 1. Montaje del sistema de medición

Para medir la temperatura en el prototipo de incubadora neonatal a escala, se utilizó un termistor NTC, cuya resistencia eléctrica disminuye cuando aumenta la temperatura. El sensor se conectó a una tarjeta ESP32 mediante un divisor de voltaje compuesto por el termistor y una resistencia fija de 3,3 kΩ.

El voltaje del punto medio del divisor se conectó al pin analógico GPIO 34 de la ESP32, permitiendo adquirir la señal eléctrica asociada a las variaciones de temperatura.

**Figura 1. Circuito de medición de temperatura con termistor NTC y ESP32.**

![Circuito de medición de temperatura](imagenes/circuito_temperatura.png)

### 2. Adquisición y procesamiento de la señal

La adquisición de datos se realizó mediante un programa desarrollado en Arduino IDE. En cada ciclo, la ESP32 tomó 100 muestras de voltaje y calculó su promedio para reducir las fluctuaciones de la lectura.

A partir del voltaje promedio, se calculó la resistencia del termistor mediante la ecuación del divisor de voltaje:

\[
R_{NTC}=R_F\left(\frac{V_{CC}-V_{NTC}}{V_{NTC}}\right)
\]

Donde:

- \(R_{NTC}\): resistencia calculada del termistor.
- \(R_F\): resistencia fija de 3,3 kΩ.
- \(V_{CC}\): voltaje de alimentación de 3,3 V.
- \(V_{NTC}\): voltaje medido en el punto medio del divisor.

La resistencia obtenida se utilizó para estimar la temperatura en grados Celsius mediante una función de interpolación lineal basada en puntos de calibración experimentales.

### 3. Calibración del termistor

La calibración se realizó utilizando mediciones de temperatura de referencia y sus correspondientes valores de resistencia. Se emplearon puntos de referencia aproximados de 18 °C, 24 °C, 36 °C y 37 °C para establecer intervalos de interpolación.

La temperatura calculada se consideró una estimación experimental. Las lecturas fuera del intervalo calibrado se identificaron mediante mensajes de advertencia, ya que la extrapolación no había sido validada.

### 4. Implementación del control de temperatura

La temperatura estimada se utilizó como variable de entrada para la lógica de control implementada en la ESP32. El sistema acciona un módulo relé conectado al GPIO 26, que permite controlar el elemento calefactor del prototipo.

El relé utilizado opera con lógica activa en nivel bajo: una señal `LOW` lo activa y una señal `HIGH` lo desactiva.

La lógica de control se configuró de la siguiente manera:

- **Temperatura inferior a 36 °C:** se solicita calentamiento.
- **Temperatura igual o superior a 37 °C:** se desactiva el calentamiento.
- **Temperatura igual o superior a 37,5 °C:** se mantiene el calentamiento desactivado y se genera una alerta de temperatura alta.

Se incorporó histéresis para reducir las conmutaciones repetitivas del relé cerca del límite de control. Si se detecta una lectura eléctrica anómala o una resistencia fuera del intervalo calibrado, el programa desactiva el relé y muestra un mensaje de advertencia.

**Figura 2. Montaje físico del sistema de control de temperatura.**

![Montaje físico del sistema de temperatura](imagenes/montaje_temperatura.jpg)

### 5. Indicadores visuales y supervisión

Se utilizaron dos LED para indicar el estado del sistema. El LED verde representa el estado de calentamiento desactivado, mientras que el LED rojo indica una solicitud de calor o una condición de advertencia.

El monitor serie de Arduino IDE permite visualizar el voltaje medido, la resistencia calculada, la temperatura estimada y el estado del relé durante el funcionamiento del prototipo.

**Figura 3. Lecturas de temperatura y estado del relé en el monitor serie.**

![Lecturas del monitor serie](imagenes/monitor_serie.png)

### 6. Verificación del funcionamiento

Se realizaron pruebas para comprobar la adquisición de la señal del termistor y la respuesta del relé ante las órdenes de activación y desactivación. También se verificó que el programa identificara lecturas anómalas y mantuviera el calentamiento desactivado ante estas condiciones.

Para evaluar la precisión de la medición, es necesario comparar la temperatura estimada por el sistema con la obtenida mediante un termómetro independiente en diferentes puntos del intervalo de operación. Por ello, la calibración debe considerarse provisional hasta completar esta validación.

**Nota:** El sistema desarrollado corresponde a un prototipo académico a escala y no está validado para uso clínico ni para controlar la temperatura de un recién nacido.
