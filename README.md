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

## Preguntas
### Pregunta 3. ¿Qué semejanzas hay entre una incubadora neonatal y una servo-cuna?

Tanto la incubadora neonatal y la servo-cuna son dispositivos que proporcionan apoyo térmico al recién nacido, para mantener una temperatura corporal adecuada. Ambos equipos incorporan sensores de temperatura, sistemas de calentamiento y mecanismos de control que permiten regular el aporte de calor según las condiciones necesitadas [1], [2].

La principal diferencia está en su estructura y forma de transferencia de calor. La incubadora neonatal proporciona un ambiente cerrado y controlado, y la servo-cuna abierta y permite un acceso más directo al recién nacido durante los procedimientos médicos. [2], [3].

## Costos del prototipo

A continuación, se presenta el presupuesto estimado de los materiales y componentes utilizados para la construcción de la incubadora neonatal a escala. Los precios están expresados en pesos colombianos (COP) y corresponden a referencias comerciales y estimaciones presupuestales.

| N.º | Material o componente | Cantidad | Precio unitario (COP) | Precio total (COP) |
|---:|---|---:|---:|---:|
| 1 | ESP32 DevKit V1 | 1 | $28.000 | $28.000 |
| 2 | Termistor NTC | 1 | $12.000 | $12.000 |
| 3 | Módulo relé de 5 V | 1 | $11.000 | $11.000 |
| 4 | Bombillo de 100 W | 1 | $4.200 | $4.200 |
| 5 | Ventilador pequeño de corriente continua | 1 | $12.875 | $12.875 |
| 6 | Láminas de acrílico transparente | 1 lote | $70.000 | $70.000 |
| 7 | Resistencia fija de 3,3 kΩ | 1 | $500 | $500 |
| 8 | LED indicadores | 3 | $500 | $1.500 |
| 9 | Protoboard | 1 | $8.000 | $8.000 |
| 10 | Cables jumper | 1 juego | $6.000 | $6.000 |
| 11 | Portalámparas y cableado | 1 juego | $10.000 | $10.000 |
| 12 | Interruptor y fusible | 1 juego | $8.000 | $8.000 |
| 13 | Cable USB para programación | 1 | $5.000 | $5.000 |
| 14 | Base y estructura de soporte | 1 lote | $25.000 | $25.000 |
| 15 | Pegamento, tornillos y elementos de fijación | 1 lote | $10.000 | $10.000 |
| | **Costo total estimado** | | | **$212.075 COP** |

### Consideraciones del presupuesto

- Los precios son aproximados y pueden variar según el proveedor.
- Los valores que no cuentan con una cotización específica se consideran estimaciones presupuestales.
- No se incluyen costos de transporte, mano de obra ni herramientas.
- El presupuesto corresponde a un prototipo académico a escala y no a una incubadora neonatal certificada para uso clínico.

### Fuentes de consulta

1. [GYO Ingeniería – ESP32 DevKit V1](https://gyoingenieria.com/producto/esp32-devkit-v1).
2. [GYO Ingeniería – Componentes electrónicos](https://gyoingenieria.com/tienda/pagina/5).
3. [MercadoLibre Colombia – Termistores NTC](https://listado.mercadolibre.com.co/termistor-ntc).
4. [Zamux – Productos eléctricos](https://zamux.co/).
5. [MercadoLibre Colombia – Componentes y ventiladores](https://www.mercadolibre.com.co/).

### Referencias

[1] Scottish Government, NHS Greater Glasgow and Clyde, “Thermal care of the neonate,” *Clinical Guidelines*. [En línea]. Disponible en: https://clinicalguidelines.scot.nhs.uk/ggc-paediatric-guidelines/ggc-paediatric-guidelines/neonatology/thermal-care-of-the-neonate-970/

[2] Royal Children's Hospital Melbourne, “Thermoregulation for neonates and infants,” *Clinical Practice Guidelines*. [En línea]. Disponible en: https://www.rch.org.au/rchcpg/hospital_clinical_guideline_index/Thermoregulation_in_the_preterm_infant/

[3] Colombia, Ministerio de Salud y Protección Social, “Decreto 438 de 2020,” *Gestor Normativo de Función Pública*. [En línea]. Disponible en: https://www1.funcionpublica.gov.co/eva/gestornormativo/norma.php?i=110716
