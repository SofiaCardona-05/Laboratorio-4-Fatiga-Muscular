
# PARTE B. Resultados experimentales

## 1. Objetivo

Verificar el funcionamiento del monitor de signos vitales Mindray uMEC 100 mediante la simulación de diferentes condiciones fisiológicas con el simulador Pronk OxSim OX-1, evaluando la respuesta de las alarmas visuales y sonoras, la señal fotopletismográfica y la precisión de las mediciones de frecuencia cardíaca y saturación periférica de oxígeno (SpO2).

## 2. Equipos utilizados

- Monitor de signos vitales Mindray uMEC 100.
- Simulador de parámetros hemodinámicos Pronk OxSim OX-1.
- Sensor de pulsioximetría (SpO2).
- Cables de conexión correspondientes.

## 3. Procedimiento experimental

### 3.1. Configuración inicial

Se encendió el monitor Mindray uMEC 100 y se seleccionó el modo de operación monitor. Posteriormente, se conectó el sensor de pulsioximetría al simulador Pronk OxSim OX-1 para generar las señales correspondientes a las pruebas.

### 3.2. Prueba 1: Simulación de bradicardia

Se configuró el simulador OxSim para representar una condición de bradicardia, estableciendo una frecuencia cardíaca de 40 bpm y una saturación de oxígeno del 95%.

Se observaron los valores registrados por el monitor uMEC 100 y la forma de onda fotopletismográfica.

**Resultados observados:**
- Frecuencia cardíaca simulada: 40 bpm.
- SpO2 simulada: 95%.
- Frecuencia cardíaca indicada por el monitor: 39 bpm.
- SpO2 indicada por el monitor: 96%.

![Prueba de bradicardia](imagenes/01_Configuracion_Bradicardia.jpg)

### 3.3. Prueba 2: Alarma por saturación baja de oxígeno

Se configuró el límite inferior de alarma de SpO2 del monitor en 90%.

Posteriormente, se ajustó el OxSim para simular una frecuencia cardíaca de 80 bpm y una SpO2 de 85%. A partir de este momento se esperaron 5 segundos, tal como lo establece la guía, y se verificó la activación de la alarma visual y sonora.

**Resultados observados:**
- Frecuencia cardíaca simulada: 80 bpm.
- SpO2 simulada: 85%.
- Límite inferior configurado: 90%.
- Alarma visual: se observó la indicación de alarma por SpO2 inferior al límite.
- Alarma sonora: se verificó durante la prueba.

![Alarma por saturación baja](imagenes/02_Alarma_SpO2_Baja.jpg)

### 3.4. Prueba 3: Simulación de baja perfusión (Low Perfusion)

Se configuró el límite superior de alarma de SpO2 en 97%. Posteriormente, se ajustó el simulador OxSim al modo Low Perfusion y se estableció una SpO2 objetivo de 99%.

Después de realizar el ajuste, se esperaron 5 segundos y se observó la respuesta del monitor, prestando atención a la lectura de SpO2, las alarmas y el comportamiento de la onda fotopletismográfica.

**Resultados observados en la fotografía:**
- SpO2 objetivo del simulador: 99%.
- Frecuencia cardíaca indicada: 80 bpm.
- SpO2 indicada por el monitor: 100%.
- Diferencia entre SpO2 objetivo e indicada: 1 punto porcentual.

En la captura se observa la señal fotopletismográfica. La lectura del monitor fue de 100%, aunque el valor configurado en el simulador era de 99%.

La activación específica de la alarma superior de SpO2 debe confirmarse con el registro de la prueba, ya que la fotografía no permite identificarla de manera inequívoca.

![Prueba Low Perfusion](imagenes/03_Low_Perfusion.jpg)

### 3.5. Prueba 4: Simulación de taquicardia

Se configuró el simulador OxSim para generar una frecuencia cardíaca de 140 bpm, manteniendo la SpO2 en 98%.

Se observó la respuesta del monitor Mindray uMEC 100 y se registró la forma de onda correspondiente.

**Resultados de referencia:**
- Frecuencia cardíaca simulada: 140 bpm.
- SpO2 simulada: 98%.

En la fotografía se observa una frecuencia cardíaca de 140 bpm y una saturación de oxígeno de 98%.

La activación de la alarma de frecuencia cardíaca elevada debe confirmarse con el registro de la prueba.

![Prueba de taquicardia](imagenes/04_Taquicardia.jpg)

## 4. Tabla de verificación de alarmas

| Prueba | Límite configurado | Valor simulado | Valor indicado por uMEC 100 | Alarma activa |
|---|---|---|---|---|
| Bradicardia | No modificado para esta prueba | FC 40 bpm / SpO2 95% | FC 39 bpm / SpO2 96% | No se documentó |
| SpO2 baja | Inferior: 90% | FC 80 bpm / SpO2 85% | FC 80 bpm / SpO2 85% | Sí, visual y sonora |
| Low Perfusion | Superior: 97% | SpO2 99% | SpO2 100% | Por confirmar |
| Taquicardia | Límite superior de FC: no documentado | FC 140 bpm / SpO2 98% | FC 140 bpm / SpO2 98% | Por confirmar |

**Nota:** En las pruebas 3 y 4 se debe completar la verificación de las alarmas con las observaciones realizadas durante el laboratorio. No se debe asumir que una alarma se activó únicamente por observar un valor en pantalla.

## 5. Cálculo de errores de medición

Para evaluar la diferencia entre los valores configurados en el simulador y los valores indicados por el monitor se utilizaron las siguientes expresiones:

**Error absoluto:**

\[
E_a=|V_{simulado}-V_{monitor}|
\]

**Error porcentual:**

\[
E_{\%}=\frac{|V_{simulado}-V_{monitor}|}{V_{simulado}}\times100
\]

Donde:

- \(V_{simulado}\): valor configurado en el OxSim.
- \(V_{monitor}\): valor indicado por el Mindray uMEC 100.

### 5.1. Resultados de los errores

| Prueba | Variable | OxSim | Mindray | Error absoluto | Error porcentual |
|---|---|---:|---:|---:|---:|
| Bradicardia | FC (bpm) | 40 | 39 | 1 | 2.50% |
| Bradicardia | SpO2 (%) | 95 | 96 | 1 | 1.05% |
| SpO2 baja | FC (bpm) | 80 | 80 | 0 | 0% |
| SpO2 baja | SpO2 (%) | 85 | 85 | 0 | 0% |
| Low Perfusion | SpO2 (%) | 99 | 100 | 1 | 1.01% |
| Taquicardia | FC (bpm) | 140 | 140 | 0 | 0% |
| Taquicardia | SpO2 (%) | 98 | 98 | 0 | 0% |

**Nota:** Los errores se calcularon a partir de las lecturas visibles en las fotografías. Los valores de la prueba Low Perfusion corresponden a la lectura observada de 100%, no a una lectura supuesta.

## 6. Registro de tiempos de respuesta

De acuerdo con el procedimiento de la guía, para las pruebas de alarma por SpO2 baja y alta se realizó una espera de 5 segundos después de ajustar el simulador.

| Prueba | Tiempo de espera indicado por la guía | Observación |
|---|---|---|
| SpO2 baja | 5 segundos | Se verificó la alarma visual y sonora. |
| Low Perfusion | 5 segundos | Se verificó la respuesta del monitor; falta confirmar la alarma específica. |

El tiempo de espera de 5 segundos corresponde al intervalo indicado en el procedimiento experimental y no necesariamente al tiempo exacto de latencia de la alarma.

## 7. Registro de señales fotopletismográficas

Durante las pruebas se observó la señal fotopletismográfica (pletismografía) representada en color verde en la pantalla del Mindray uMEC 100.

Esta señal permitió observar las variaciones pulsátiles asociadas a la actividad cardíaca y a la detección óptica de la señal de pulsioximetría.

Se registraron las siguientes condiciones:

- Bradicardia: observación de la onda durante la simulación de 40 bpm.
- SpO2 baja: observación de la onda durante la simulación de 85%.
- Low Perfusion: observación de la onda bajo condiciones de baja perfusión.
- Taquicardia: observación de la onda durante la simulación de 140 bpm.

## 8. Observaciones generales

1. El monitor Mindray uMEC 100 permitió visualizar los valores de frecuencia cardíaca y saturación de oxígeno generados por el simulador.
2. Durante la prueba de SpO2 baja se observó la activación de las alarmas visual y sonora al establecer un valor inferior al límite configurado.
3. En la prueba Low Perfusion se presentó una diferencia de un punto porcentual entre el valor configurado en el simulador y el indicado por el monitor.
4. Las formas de onda fotopletismográficas permitieron observar la respuesta del monitor ante las diferentes condiciones simuladas.
5. La evaluación de cada alarma debe considerar tanto los valores medidos como la configuración de los límites establecidos en el monitor.
