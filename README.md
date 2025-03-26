# Laboratorio-4-Fatiga-Muscular
Este laboratorio se centra en la adquisición y análisis de señales electromiográficas (EMG) para evaluar la fatiga muscular. Se utilizan técnicas de filtrado y análisis espectral para mejorar la calidad de la señal. El desarrollo se realizó en Python y los resultados se documentan en este repositorio

## ***OBJETIVOS***
Adquisición de la señal EMG: Capturar una señal electromiográfica

Filtrado de la señal: Implementar filtros pasa altas y pasa bajas

Aplicación de ventanas: Aplicar una ventana adecuada

Análisis espectral: Transformar la señal al dominio de la frecuencia mediante FFT
## ***MATERIALES***
Electrodos

DAQ (NI USB-6008)

AD8232
## ***PROCEDIMIENTO*** 
- Adquisición Señal
- frecuencia de muestreo de 1000Hz
- tiempo de muestreo de 5 segundos 
- 5000 muestras (longitud de la señal)
- Musculo  Flexor Digitorum Superficialis


## ***GRÁFICA DE LA SEÑAL***

![image](https://github.com/SofiaCardona-05/Laboratorio-4-Fatiga-Muscular/blob/main/Captura%20de%20pantalla%202025-03-25%20235419.png)

## ***Filtrado de la Señal***
Se aplicaron los siguientes filtros:

***Filtro Pasa Altas:*** Frecuencia de corte en 20 Hz.

***Filtro Pasa Bajas:*** Frecuencia de corte en 450 Hz.

***Orden del filtro:*** 4 (Butterworth).

## ***Justificación:***
El filtro pasa altas elimina ruido de baja frecuencia (movimiento del cuerpo).

El filtro pasa bajas elimina interferencias de alta frecuencia (>450 Hz).

Gráfica de la señal filtrada:
![image]()



