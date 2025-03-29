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


```python
import nidaqmx 

import numpy as np

import matplotlib.pyplot as plt

from scipy.signal import butter, filtfilt, welch

from scipy.fftpack import fft

frecuencia de muestreo de fs = 3000Hz
tiempo de muestreo = diracion = muestras/fs
9000 muestras (longitud de la señal)
Musculo  Flexor Digitorum Superficialis
canal = "Dev3/ai0" 

with nidaqmx.Task() as task:
    task.ai_channels.add_ai_voltage_chan(canal, min_val=-10.0, max_val=10.0)  
    task.timing.cfg_samp_clk_timing(fs, samps_per_chan=fs*tiempoa)
    datos = task.read(number_of_samples_per_channel=fs*tiempoa)
    datos = np.array(datos)

tiempo = np.linspace(0, tiempoa, len(datos))

```
- frecuencia de muestreo de fs = 3000Hz
- tiempo de muestreo = diracion = muestras/fs
- 9000 muestras (longitud de la señal)
- Musculo  Flexor Digitorum Superficialis


## ***GRÁFICA DE LA SEÑAL***

![image](https://github.com/SofiaCardona-05/Laboratorio-4-Fatiga-Muscular/blob/main/WhatsApp%20Image%202025-03-28%20at%2022.35.11.jpeg)

```python
plt.figure(figsize=(10, 4))
plt.plot(tiempo, datos)
plt.xlabel("Tiempo (s)")
plt.ylabel("Voltaje (V)")
plt.title("Señal EMG")
plt.grid()
plt.show()
```

## ***Filtrado de la Señal***
Se aplicaron los siguientes filtros:

***Filtro Pasa Altas:*** Frecuencia de corte en 80 Hz.

***Filtro Pasa Bajas:*** Frecuencia de corte en 120 Hz.
-Entre 80 Hz y 120 Hz trabajan intensamente las fibras rápidas, estas son frecuencias que permiten capturar la señal ECG
Orden del filtro: 2 (Butterworth).
```python
def butterworth_filter(data, cutoff, fs, order=4, filter_type='high'):
    nyquist = 0.5 * fs  
    normal_cutoff = cutoff / nyquist
    b, a = butter(order, normal_cutoff, btype=filter_type, analog=False)
    return filtfilt(b, a, data)
```
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


## ***Justificación:***
-El filtro pasa altas elimina ruido de baja frecuencia que pueden deberse a movimiento del cuerpo. La idea es eliminar frecuencias menores s 20Hz dejando pasar las frecuencias mayores a 20Hz

-El filtro pasa bajas elimina interferencias de alta frecuencia menores a 450 Hz.

## ***Gráfica de la señal filtrada:***
```python
plt.figure(figsize=(10, 4))
plt.plot(tiempo, datos_filtrados, label="Señal Filtrada")
plt.xlabel("Tiempo (s)")
plt.ylabel("Voltaje (V)")
plt.title("Señal EMG Filtrada")
plt.grid()
plt.show()
```
![image](https://github.com/SofiaCardona-05/Laboratorio-4-Fatiga-Muscular/blob/main/WhatsApp%20Image%202025-03-26%20at%2012.24.09%20AM.jpeg)

***NOTA:*** Se observa que la señal filtrada y la señal original son muy similares. Esto puede deberse a que el sistema de adquisición de datos DAQ NI USB-6008 aplica un preprocesamiento interno que reduce el ruido antes de la captura. Además, la señal EMG adquirida no presentaba una cantidad significativa de ruido en las bandas eliminadas por los filtros pasa altos y bajos, lo que explica la mínima diferencia visual entre ambas señales.

## ***Análisis Espectral***
Se aplicó la Transformada Rápida de Fourier para obtener la frecuencia mediana.
```python
N = len(datos_filtrados)  
frecuencias = np.fft.fftfreq(N, d=1/fs)  
transformada = np.abs(fft(datos_filtrados)) 


plt.figure(figsize=(10, 4))
plt.plot(frecuencias[:N//2], transformada[:N//2], color='g')
plt.xlabel("Frecuencia (Hz)")
plt.ylabel("Amplitud")
plt.title("Espectro de Frecuencia")
plt.grid()
plt.show()

frecuencias_welch, densidad_potencia = welch(datos_filtrados, fs, nperseg=1024)
frecuencia_mediana = frecuencias_welch[np.where(np.cumsum(densidad_potencia) >= np.sum(densidad_potencia) / 2)[0][0]]
```

***Parámetros analizados:***
- Frecuencia dominante: 45.90 Hz.
- Frecuencia media: 45.80 Hz.
- Desviación estándar: 10.19 Hz.
  
## ***Gráfica del espectro de frecuencia:***
![image](https://github.com/SofiaCardona-05/Laboratorio-4-Fatiga-Muscular/blob/main/WhatsApp%20Image%202025-03-26%20at%2012.24.32%20AM.jpeg)

## ***Grafica de evolucion de la frecuencia***
```python
ventana = 1
muestras = int(fs * ventana)  
num_ventanas = len(datos_filtrados) // muestras  

frecuencias_medianas = []


for i in range(num_ventanas):
    inicio = i * muestras
    fin = inicio + muestras
    segmento = datos_filtrados[inicio:fin]
    
    if len(segmento) == muestras:
        f_welch, p_welch = welch(segmento, fs, nperseg=256)
        f_mediana = f_welch[np.where(np.cumsum(p_welch) >= np.sum(p_welch) / 2)[0][0]]
        frecuencias_medianas.append(f_mediana)


plt.figure(figsize=(10, 4))
plt.plot(np.arange(len(frecuencias_medianas)), frecuencias_medianas, marker='o', linestyle='-', color='m')
plt.xlabel("Tiempo (ventanas)")
plt.ylabel("Frecuencia Mediana (Hz)")
plt.title("Evolución de la Frecuencia")
plt.grid()
plt.show()
```
![image](https://github.com/SofiaCardona-05/Laboratorio-4-Fatiga-Muscular/blob/main/WhatsApp%20Image%202025-03-26%20at%2012.24.50%20AM.jpeg)

## ***Análisis de Resultados:***

Los resultados obtenidos muestran una tendencia decreciente en la frecuencia mediana a lo largo del tiempo, lo que sugiere la presencia de fatiga muscular en el músculo analizado. La disminución de la frecuencia mediana indica una reducción en la activación de fibras musculares rápidas. Además, el análisis espectral evidencia un desplazamiento de la energía hacia frecuencias más bajas, confirmando el proceso de fatiga.

## ***Conclusiones***

- La adquisición de la señal EMG se realizó con éxito, permitiendo capturar la actividad eléctrica del músculo analizado.

- El uso de la Transformada de Fourier permitió caracterizar la señal en el dominio de la frecuencia, facilitando la identificación de patrones relacionados con la fatiga muscular.

- La disminución progresiva de la frecuencia mediana confirma la presencia de fatiga muscular, indicando un cambio en la activación de las fibras musculares.





