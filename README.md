# Laboratorio 4 Fatiga Muscular
Este laboratorio se centra en la adquisición y análisis de señales electromiográficas (EMG) para evaluar la fatiga muscular. Se utilizan técnicas de filtrado y análisis espectral para mejorar la calidad de la señal. El desarrollo se realizó en Python y los resultados se documentan en este repositorio.

## ***OBJETIVOS***
Adquisición de la señal EMG: Capturar una señal electromiográfica

Filtrado de la señal: Implementar filtros pasa altas y pasa bajas

Aplicación de ventanas: Aplicar una ventana adecuada

Análisis espectral: Transformar la señal al dominio de la frecuencia mediante FFT
## ***MATERIALES***
Electrodos

DAQ (NI USB-6008)

AD8232: modulo especializado para el monitoreo de señales ECG, aunque sea diseñado para ECG su puede captar señales EMG 
## ***PROCEDIMIENTO*** 
Adquisición Señal
<p align="center">
  <img src="https://github.com/SofiaCardona-05/Laboratorio-4-Fatiga-Muscular/blob/main/WhatsApp%20Image%202025-03-28%20at%2021.26.47.jpeg?raw=true" width="200"/>
</p>

- frecuencia de muestreo de fs = 3000Hz
- tiempo de muestreo = diracion = muestras/fs
- 9000 muestras (longitud de la señal)
- Musculo  Flexor Digitorum Superficialis


## ***GRÁFICA DE LA SEÑAL***

![image](https://github.com/SofiaCardona-05/Laboratorio-4-Fatiga-Muscular/blob/main/WhatsApp%20Image%202025-03-28%20at%2022.35.11.jpeg)



## ***Filtrado de la Señal***
![image](https://github.com/SofiaCardona-05/Laboratorio-4-Fatiga-Muscular/blob/main/WhatsApp%20Image%202025-03-28%20at%2023.28.34.jpeg)

Se aplicaron los siguientes filtros:

***Filtro Pasa Altas:*** Frecuencia de corte en 80 Hz.

***Filtro Pasa Bajas:*** Frecuencia de corte en 120 Hz.
-Entre 80 Hz y 120 Hz trabajan intensamente las fibras rápidas, estas son frecuencias que permiten capturar la señal ECG
Orden del filtro: 2 (Butterworth).

##Aplicación de Ventanas

Para segmentar la señal EMG antes del análisis espectral, se aplicó una ventana de tipo Hanning a cada segmento de 0.2 segundos.

La ventana de Hanning es una función de forma suave, que reduce los bordes abruptos de las ventanas, lo cual minimiza los efectos no deseados en la Transformada de Fourier (como fugas espectrales). 

### Características de la ventana:
- **Tipo**: Hanning
- **Duración**: 0.1 segundos
- **Muestras por ventana**: 300 (calculado como fs * 0.1 con fs = 3000 Hz)

<p align="center">
  <img src="https://github.com/user-attachments/assets/c9598a6a-44a6-489c-b640-599d6ca3c7df" width="500"/>
</p>


## ***Analisis espectral***
![image](https://github.com/SofiaCardona-05/Laboratorio-4-Fatiga-Muscular/blob/main/WhatsApp%20Image%202025-03-28%20at%2022.40.12.jpeg)

Se presenta el espectro de frecuencias de la ventana 298 de la señal EMG. El análisis espectral se realizó con la Transformada Rápida de Fourier (FFT)
En este espectro se puede observar que:

- La frecuencia dominante se encuentra cerca de los 100 Hz, lo cual es típico de una señal EMG activa.
- La magnitud más alta 850.
- El resto de la energía está distribuida en componentes de menor magnitud, lo que es coherente con la actividad muscular registrada.

## Resultados y Análisis Estadístico

Tras aplicar el análisis espectral a cada ventana de la señal EMG filtrada y segmentada con ventanas de Hanning. 

Se realizó una prueba de diferencia de medias entre las frecuencias medianas del inicio y del final del experimento. Esta prueba permite determinar si hay una disminución significativa de la frecuencia, lo cual es un indicador de fatiga muscular.

Sin embargo, en este caso no fue posible aplicar la prueba estadística debido a que los datos no presentaban variación (frecuencia mediana constante en todas las ventanas analizadas).

---

### Hipótesis estadística

- **Hipótesis nula (H₀):** No hay diferencia significativa entre las frecuencias medianas al inicio y al final del ejercicio.
- **Hipótesis alternativa (H₁):** La frecuencia mediana disminuye significativamente al final del ejercicio, lo que sugiere fatiga muscular.

---

### Conclusión

Durante el análisis espectral de la señal EMG, se observó que la frecuencia mediana se mantuvo constante en todas las ventanas analizadas, con un valor estable de 750.0 Hz.

Esto indica que no se detectaron signos de fatiga muscular, ya que uno de los indicadores clásicos de fatiga es la disminución progresiva de la frecuencia mediana a lo largo del tiempo. Al no presentarse dicha disminución, la señal se considera estable desde el punto de vista espectral.

Debido a esta ausencia total de variación en los valores, no fue posible aplicar una prueba estadística (como el test de diferencia de medias), ya que este tipo de análisis requiere que exista al menos una mínima dispersión en los datos para comparar dos grupos.

---


### Otras graficas




