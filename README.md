# **Laboratorio 5: Variabilidad de la Frecuencia Cardíaca HRV y balance autonómico**

## Integrantes
* Laura Valentina Velásquez Castiblanco (5600846)
* Carol Valentina Cruz Becerra (5600845)
* Carlos Felipe Moreno Guzmán (5600881)

## Objetivos:
* Identificar cambios en el balance autonómico mediante análisis temporal de la variabilidad de la frecuencia cardíaca (HRV).
* Detectar los picos R y calcular los diferentes intervalos R-R.
* Realizar el diagrama de Poincare para la señal ECG.

## Diagramas de flujo

> ### Parte A: Preparación del Paciente y Entorno 

<p align="center">
<img width="581" height="1000" alt="image" src="https://github.com/user-attachments/assets/f670291b-e851-4386-a4d7-662e86498336" />
</p>

> ### Parte B

<p align="center">
<img width="581" height="1470" alt="image" src="https://github.com/user-attachments/assets/b80f84c4-1d34-4250-bc73-abc9400fb864" />
</p>

> ### Parte C

<p align="center">
<img width="581" height="897" alt="image" src="https://github.com/user-attachments/assets/00c6d5d7-1e78-46f2-9d50-fa735171b7ea" />
</p>

## Configuración inicial

Para la parte B y C se necesita el uso de librerias: 

```python
from google.colab import drive
import numpy as np
import matplotlib.pyplot as plt
from scipy import signal
from scipy.signal import find_peaks
```

# **Parte A**

## a. Fundamento Teórico

### **Actividad Simpática y Parasimpática del Sistema Nervioso Autónomo**

El **Sistema Nervioso Autónomo** (SNA) regula los procesos fisiológicos del cuerpo humano sin control consciente, es decir, de manera completamente automática. El SNA se divide en dos principales ramas:

> #### **Sistema Nervioso Simpático (SNS)**

Se encarga de preparar al organismo para situaciones de **alerta, actividad física, estrés, peligro, ansiedad o dolor**. Se le conoce también como el sistema de **respuesta - huida**. Es un sistema de carácter **excitatorio**, que aumenta el rendimiento general del cuerpo para responder de manera rápida y efectiva a los estímulos. Los neurotransmisores característicos de la actividad simpática son:

* Acetilcolina (ACh)
* Noradrenalina (NE)
* Adrenalina (EPI)
* Dopamina (DA)

Unos de los efectos de la actividad simpática son; aumento del gasto cardíaco, aumento de la disponibilidad energética (glucósa, ácidos grasos) e inhibición de funciones no escenciales (como la digestión).

> #### **Sistema Nervioso Parasimpático (SNP)**

Su principal objetivo es **mantener la homeostasis del cuerpo en condiciones de reposo**. Este sistema promueve la conservación de la energía, la recuperación funcional de los órganos y procesos importantes como la nutrición, el crecimiento y la reparación. La actividad parasimpática favorece el estado de calma fisiológica y su principal neurotransmisor es la **Acetilcolina**.

Algunos efectos generados por la actividad parasimpática son; diminución del gasto cardíaco, bronco-constricción, aumento de actividad digestiva y estimulación de la digestión.

---

### **Efecto de actividad Simpática y Parásimpatica en la frecuencia cardíaca**

La **actividad simpática aumenta la frecuencia cardíaca**. El SNS libera noradrenalina, la cual activa receptores $\beta 1$-adrenérgicos en el nodo SA que permiten que las células alcancel el umbral más rápido, aumentando velocidad de conducción en el nodo AV. En conjunto, el corazón late más rápido (taquicardia) y más fuerte para suplir la demanda de sangre extra debido a estímulos como actividad física o estrés.

La **actividad parasimpática disminuye la frecuencia cardíaca**. El SNP libera acetilcolina sobre receptores muscarínicos en el nodo SA, reduciendo la pendiente de la despolarización e hiperpolarizando la membrana para así retardar la coducción en el nodo AV. De esta manera, el corazón late más lento y con menor excitabilidad, permitiendo que el organismo descanse y conserve la mayor cantidad de energía posible.

---

### **Variabilidad de la Frecuencia Cardíaca (HRV) a partir de un ECG**

La HRV es una medida que indica cuánta variabilidad se presenta entre los intervalos R-R de un electrocardiograma, entre los latidos del corazón. Esta variabilidad representa el **equilibrio entre el sistema simpático y el sistema parasimpático**. Esta medida puede ser empleada en entornos clínicos, deportivos e incluso científicos, ya que permite evaluar estrés fisiológico o emocional, detectar fatiga o sobreentrenamiento y determinar un indicador de carácter pronóstico en cardiología.

Calcular la HRV a partir de un ECG se basa en realizar análisis tanto en el dominio del tiempo como en el de la frecuencia partiendo de la obtención de parámetros relevantes de la señal:

1. **Detección de Picos R:** Máximos del complejo QRS.
2. **Extracción intervalos R-R:** En milisegundos ($ms$).

Posteriormente, con los anteriores datos ya almacenados, se procede a realizarse el análisis en tiempo o frecuencia correspondiente.

> Dominio del Tiempo ($t$)

* **SDNN:** Variabilidad total del SNA.
* **RMSSD:** Cambios rápidos entre latidos (parasimpático).
* **pNN50:** R-R superando $50$ $ms$ (parasimpático).

> Dominio de la Frecuencia ($f$)

* **VLF (Very Low Frequency):** Procesos fisiológicos muy lentos.
* **LF (Low Frecuency):** Combinación simpática y parasimpática.
* **HF (High Frecuency):** Arritmia sinusal (parasimpático).
* **LF/HF:** Alto = simpático, Bajo = parasimpático.

Posteriormente, estos dos formatos de análisis se integran para describir de forma completa la HRV e identificar dominio simpático o parasimpático en el paciente.

---

### **Diagrama de Poincaré; análisis de series R-R**

El _**Diagrama de Poincaré**_ o _**Poincaré Plot**_ en inglés es una herramienta no lineal ampliamente utilizada para analizar la serie de intervalos R-R y caracterizar la HRV. Su construcción es relativamente sencilla y requiere haber definido previamente la lista de los tiempos (en $ms$) en los que se detectaron los R-R: 

Ej. ``[RR(n), RR(n+1), RR(n+2), RR(n+3), ..., R(n+m)]``

Así, para cada punto coordendo del diagrama, se ubica en el eje $x$ (horizontal) un intervalo R-R `RR(n)` y en el eje $y$ (vertical) el intervalo R-R siguiente `RR(n+1)`. Esta configuración generará un diagrama de dispersión que permite ver patrones dinámicos que son difíciles de captar con análisis lineales simples. 

<p align="center">
<img width="462" height="443" alt="image" src="https://github.com/user-attachments/assets/f05ff933-3ba7-4445-89c4-fa2fb48a3a72" />
</p>

La cuantificación de esta dispersión puede realizarse mediante un ajuste de elipse alrededor de la línea de identidad (recta donde $RR_n = RR_{n+1}$). Esta define dos parámetros importantes:

* **SD1:** Variabilidad a corto plazo (actividad parasimpática).
* **SD2:** Variabilidad a largo plazo (más simpático que SD1).<br>

<p align="center">
<img width="600.8" height="499.2" alt="image" src="https://github.com/user-attachments/assets/71395f79-e163-428c-b3fc-4f180b7a3dcf" />
</p>

Todas estas herramientas visuales y numéricas permiten realizar una interpretación fisiológica de la señal:

* **Punto muy disperso:** Alta variabilidad, buena modulación autonómica.
* **SD1 alto:** Cambio entre latidos consecutivos rápido (parasimpático).
* **SD2 alto:** Variaciones lentas (posiblemente simpático).
* **Elipse ancha:** SD2 predominante.
* **Elipse delgada:** SD1 predominante.

---

### **Papel del Balance Autonómico en la HRV**

El _**Balance Autonómico**_ es el equilibrio dinámico entre el sistema simpático y parasimpático, el cual es ajustado constántemente por nuestro organismo según las necesidades y los estímulos. La HRV refleja directamente la interacción simpático-parasimpático, por lo que es una herramienta clave para poder cuantificar el balance autonómico:

* **HRV baja:** Simpático (intervalos uniformes y rígidos).
* **HRV alta:** Parasimpático (intervalos flexibles y variables).

Esta cuantificación permite identificar un balance adecuado, o un desbalance entre los dos sistemas. Lo anterior facilita la identificación de patrones relacionados con el manejo del estrés, salud cardiovascular y recuperación fisiológica (entre otros) en los pacientes, ofreciendo marcadores de gran utilidad para el personal médico.

## b. Adquisición de la señal ECG

Se seleccionó un sujeto de prueba para la adquisición de la señal electrocardiográfica. Se registró la actividad del ECG durante un total de 4 minutos: durante los primeros 2 minutos, el participante permaneció inmóvil y en completo silencio, mientras que en los últimos 2 minutos leyó en voz alta un fragmento de texto previamente elegido por el equipo. Además, se verificó que la frecuencia de muestreo y los niveles de cuantificación configurados fueran adecuados para garantizar la correcta captura y el análisis de la señal.

En este bloque se define la ruta del archivo que contiene la señal ECG almacenada en formato de texto. La variable ``file_path`` guarda la ubicación del archivo dentro de Google Drive. Luego, la función ``np.loadtxt()`` lee el archivo y carga los datos numéricos en la variable ``signal``, quedando disponibles como un arreglo de ``NumPy`` para su posterior procesamiento.

```python
file_path = '/content/drive/MyDrive/Colab Notebooks/Lab Procesamiento Digital de Señales/PDS - Lab 5/ECGLab5_5000.txt'
signal = np.loadtxt(file_path)
```

Este fragmento crea la gráfica de la señal ECG cargada previamente. Se genera un gráfico de la señal completa usando ``plt.plot(signal)``. Después se añade un título descriptivo y etiquetas para los ejes, indicando que el eje horizontal representa el número de muestras y el vertical la amplitud medida en voltios. También se activa una cuadrícula para facilitar la lectura de la gráfica. La instrucción ``plt.xlim(5000, 15000)`` limita el eje horizontal para visualizar un segmento específico de la señal (entre las muestras 5000 y 15000). Finalmente, ``plt.show()`` muestra la figura en pantalla.

```python
plt.figure(figsize=(12, 6))
plt.plot(signal)
plt.title('Señal ECG - 4 minutos')
plt.xlabel('Muestras (n)')
plt.ylabel('Amplitud (V)')
plt.grid(True)
plt.xlim(5000, 15000)
plt.show()
```
<p align="center">
<img width="70%" height="547" alt="image" src="https://github.com/user-attachments/assets/1e9eeb0b-4596-4a89-b3d0-7f7230b64c8f" />
</p>

# **Parte B**
## c. Pre-procesamiento de la señal

Para garantizar una correcta interpretación de la señal electrocardiográfica (ECG), es necesario eliminar el ruido producido por el movimiento, la respiración y la deriva de la línea base. En este laboratorio se adquirió la señal ECG de un sujeto durante cuatro minutos: dos en reposo y dos leyendo en voz alta, verificando previamente que la frecuencia de muestreo y la cuantificación fueran adecuadas.

Posteriormente, se diseñaron e implementaron dos filtros digitales IIR: un filtro pasa-alto para corregir la deriva de baja frecuencia y un filtro pasa-banda para resaltar el contenido espectral propio del ECG. Finalmente, se obtuvo la ecuación en diferencias de cada filtro y se aplicaron a la señal asumiendo condiciones iniciales en cero.

### 1. Filtro HP IIR 

>### 1.1. Diseño del Filtro

>### Parámetros

En esta primera etapa se establecen los parámetros principales del filtro IIR pasa-altos. Se definen las frecuencias límite ``f₁ = 0.5 Hz`` y ``f₂ = 2 Hz``, que corresponden al inicio de la banda de rechazo y de la banda de transición, respectivamente. También se especifican las atenuaciones requeridas para cada banda, siendo ``k₁ = −10 dB`` en la banda de rechazo y ``k₂ = −3 dB`` en la banda de transición. 

Estos valores constituyen la base sobre la cual se calculará el orden del filtro y su comportamiento deseado en frecuencia.

<p align="center">
<img width="885" height="660" alt="image" src="https://github.com/user-attachments/assets/8ffc071e-ce9f-49ea-b28f-c10796bc3f6d" />
</p>

>### Pasar a Requisitos Digitales

Luego se trasladan las frecuencias analógicas al dominio digital mediante la normalización con la frecuencia de muestreo, que en este caso es de ``5000 muestras por segundo``. A partir de esta conversión se obtienen las frecuencias digitales equivalentes ``ω₁ = 6.28×10⁻⁴ rad/muestra`` y ``ω₂ = 25.14×10⁻⁴ rad/muestra``. 

Estos valores permiten definir con precisión las bandas del filtro dentro del dominio discreto en el cual será implementado.

<p align="center">
<img width="513" height="196" alt="image" src="https://github.com/user-attachments/assets/7394a8d7-46f5-4307-94db-dd68c7fe420d" />
</p>

>### T1 y Pre-Warping

Debido a la distorsión que introduce la transformación bilineal, se aplica el proceso de pre-warping con la expresión ``Ω = 2·tan(ω/2)``. Este procedimiento permite corregir las frecuencias digitales anteriores y obtener las versiones ajustadas ``Ω₁ = 6.28×10⁻⁴`` y ``Ω₂ = 25.14×10⁻⁴``. Estas frecuencias corregidas garantizan que, una vez realizada la transformación al dominio Z, el filtro digital mantenga las características especificadas en el diseño analógico original.

<p align="center">
<img width="535" height="129" alt="image" src="https://github.com/user-attachments/assets/92541e15-077c-46ec-9700-7b8ad359dc20" />
</p>

>### Filtro Análogo

Con las frecuencias corregidas se determinan los valores normalizados ``Ωᵣ = 4 rad/s`` y ``Ωₚ = 1 rad/s``, que representan las fronteras de la banda de rechazo y la banda de paso en el diseño analógico. A partir de estos valores y de las atenuaciones definidas, se calcula que el filtro requerido es de primer orden. Posteriormente se obtiene la función de transferencia analógica correspondiente, la cual adopta la forma pasa-altos y constituye la base previa a la digitalización completa del filtro.

<p align="center">
<img width="608" height="541" alt="image" src="https://github.com/user-attachments/assets/388bd74f-12ee-466f-ae74-422ae8540a46" />
</p>

>### Transformación Bilineal
Para llevar el filtro al dominio Z se reemplaza la variable analógica **s** por su forma bilineal equivalente: ``s = 2·(1 − z⁻¹) / (1 + z⁻¹)``. Tras esta sustitución y la correspondiente simplificación algebraica, se obtiene una expresión discreta de la función de transferencia. En este desarrollo aparecen coeficientes numéricos relevantes como ``2.002514`` y ``1.997486``, así como términos dependientes de ``z⁻¹``, que permiten identificar y extraer directamente los coeficientes finales del filtro digital.

<p align="center">
<img width="798" height="327" alt="image" src="https://github.com/user-attachments/assets/527594f8-28be-4c12-9bd5-2978e902c54e" />
</p>

>### Ecuación en Diferencias

Finalmente, a partir de la función ``H(z)`` obtenida, se despeja la ecuación en diferencias que define cómo el filtro procesa cada muestra. La ecuación resultante es: ``y(n) = 0.998744·x(n) − 0.998744·x(n−1) + 0.997489·y(n−1)``. Los coeficientes ``0.998744`` y ``0.997489`` representan los valores exactos obtenidos en el cálculo del filtro. Esta relación recursiva describe cómo la salida actual depende tanto de las entradas actual y pasada como de la salida previa, finalizando así la implementación digital del filtro pasa-altos.

<p align="center">
<img width="651" height="335" alt="image" src="https://github.com/user-attachments/assets/8a510ad4-f0c3-489e-b5e8-fb66751ddfc6" />
</p>

>### 1.2. Implementación en Python

La función ``IIR_HP(x)`` implementa en código el filtro IIR pasa-altos que se obtuvo previamente mediante el diseño analítico. Para ello, comienza creando un vector de salida del mismo tamaño que la señal de entrada y definiendo los coeficientes del filtro, los cuales corresponden directamente a la ecuación en diferencias derivada de la función de transferencia digital. Además, inicializa dos memorias (``x1`` y ``y1``) que almacenan la entrada y la salida anteriores, necesarias debido al carácter recursivo del filtro IIR. Luego, en cada iteración del bucle recorre la señal muestra por muestra, calculando la salida actual como combinación lineal de la entrada presente, la entrada pasada y la salida previa. Después de cada cálculo actualiza las memorias para la siguiente iteración, permitiendo así mantener la continuidad del proceso recursivo. Al finalizar, la función devuelve el vector ``y``, que contiene la señal filtrada según las características del filtro pasa-altos diseñado.

```python
# Pasa-Altos
def IIR_HP(x):

    y = np.zeros_like(x)

    # Coeficientes del filtro
    b0 = 0.998744
    b1 = -0.998744
    a1 = 0.997489

    # Memorias
    x1 = 0
    y1 = 0

    for n in range(len(x)):
        y[n] = b0*x[n] + b1*x1 + a1*y1

        # Actualizar memorias
        x1 = x[n]
        y1 = y[n]

    return y
```

### 2. Filtro LP IIR 

>### 2.1. Diseño del Filtro

>### Parámetros - Pasar a Requisitos Digitales

En esta sección se definen los parámetros iniciales para el diseño del filtro FIR pasa-bajos, incluyendo los valores de 𝑘1=−3 dB y 𝑘2=−18 dB, así como las frecuencias de corte relacionadas con los índices 128 y 208. Estos parámetros sirven como base para calcular las frecuencias normalizadas y los requerimientos del filtro.
Posteriormente, se convierten las frecuencias analógicas a digitales dividiéndolas por la frecuencia de muestreo (5000 muestras/s). Esto da como resultado valores como 𝑊1=0.151rad/muestra y 𝑊2=0.251rad/muestra, que representan los límites de la banda de paso y de transición del filtro.

<p align="center">
<img width="689" height="288" alt="image" src="https://github.com/user-attachments/assets/51fa572f-c955-4fcd-a14f-57ba9dcde36b" />
</p>

>### T1 y Pre-Warping

Se aplica la corrección por pre-warp usando la fórmula Ω=2tan(𝜔/2). A partir de los valores digitalizados, se obtienen frecuencias corregidas como Ω1=0.15 y Ω2=0.252	​, que compensan la distorsión generada por la transformación bilineal.

<p align="center">
<img width="364" height="177" alt="image" src="https://github.com/user-attachments/assets/efe55343-760b-4a2c-bec5-673ec3d51dad" />
</p>

>### Filtro Análogo

Con las frecuencias corregidas se calcula el orden del filtro usando la expresión logarítmica, obteniéndose 𝑛=2. Luego se determina la función de transferencia analógica.

<p align="center">
<img width="793" height="634" alt="image" src="https://github.com/user-attachments/assets/a7f67030-b79e-43b5-b664-0b8c04589ce8" />
</p>

>### Transformación Bilineal

En esta etapa se sustituye la variable s por su equivalente bilineal, definido como: s = 2(1 − z⁻¹) / (1 + z⁻¹). Esta transformación permite obtener la función de transferencia en el dominio Z. Durante el proceso aparecen coeficientes característicos del filtro digital, tales como 3.44×10⁻³, 1.032×10⁻² y 3.94×10⁻³, los cuales conforman los parámetros finales del filtro implementado.

<p align="center">
<img width="1648" height="785" alt="image" src="https://github.com/user-attachments/assets/bafea7d0-4eb4-4958-a4c4-a3a204219492" />
</p>

>### Ecuación en Diferencias

Finalmente, a partir de la función H(z) se despeja la ecuación en diferencias que implementa el filtro. En esta expresión aparecen coeficientes característicos como 3.304, -7.118, 4.718 y -0.876, que multiplican las salidas anteriores ``y(n−1)``, ``y(n−2)`` y ``y(n−3)``. También se identifican los coeficientes asociados a las entradas: 3.44×10⁻³, 1.032×10⁻² y nuevamente 3.44×10⁻³. Esta ecuación describe cómo se obtiene cada nueva muestra del filtro FIR/LB a partir de combinaciones lineales de entradas y salidas previas.

<p align="center">
<img width="1780" height="415" alt="image" src="https://github.com/user-attachments/assets/2518aa97-3490-493a-b6b2-062859ef7d6e" />
</p>

>### 2.2. Implementación en Python

La función ``IIR_LP(x)`` implementa un filtro IIR pasa-bajos de tercer orden utilizando la ecuación en diferencias obtenida en el diseño del filtro. Para ello, se inicializa un vector de salida del mismo tamaño que la señal de entrada y se definen los coeficientes del filtro: los coeficientes ``b0``, ``b1``, ``b2`` y ``b3`` asociados a las entradas actual y pasadas, y los coeficientes ``a1``, ``a2`` y ``a3`` correspondientes a las salidas previas. Además, se crean memorias para almacenar las últimas tres entradas ``(x1, x2, x3)`` y las últimas tres salidas ``(y1, y2, y3)``, necesarias para la implementación recursiva del filtro. En cada iteración del bucle, la salida actual ``y[n]`` se calcula como una combinación lineal de las entradas presentes y anteriores junto con las salidas pasadas, aplicando directamente la ecuación en diferencias del filtro. Tras cada cálculo, las memorias se actualizan desplazando las muestras previas para su uso en la siguiente iteración. Finalmente, la función devuelve el vector y, que representa la señal procesada por el filtro pasa-bajos.

```python
# Pasa-Bajo
def IIR_LP(x):

    y = np.zeros_like(x)

    # Coeficientes x
    b0 = 1.04e-3
    b1 = 3.12e-3
    b2 = 3.12e-3
    b3 = 1.04e-3

    # Coeficientes y
    a1 = 2.154
    a2 = -1.425
    a3 = 0.2654

    # Memorias (entradas y salidas pasadas)
    x1 = 0;  x2 = 0;  x3 = 0
    y1 = 0;  y2 = 0;  y3 = 0

    for n in range(len(x)):
        y[n] = (b0*x[n] + b1*x1 + b2*x2 + b3*x3
                + a1*y1 + a2*y2 + a3*y3)

        # Actualizar memorias de entrada
        x3 = x2
        x2 = x1
        x1 = x[n]

        # Actualizar memorias de salida
        y3 = y2
        y2 = y1
        y1 = y[n]

    return y
```

### 3. Aplicación de los Filtros

El fragmento de código aplica dos filtros IIR en cascada a una señal ECG y posteriormente grafica el resultado filtrado. Primero, la señal original ``signal`` pasa por el filtro pasa-altos ``IIR_HP``, cuyo objetivo suele ser eliminar componentes de muy baja frecuencia, como el desplazamiento de línea base. Luego, la salida obtenida se procesa con el filtro pasa-bajos ``IIR_LP``, encargado de atenuar el ruido de alta frecuencia presente en el ECG.

Después del filtrado, se genera una grafica de la señal resultante. Se añaden título, etiquetas de los ejes y una cuadrícula para facilitar la visualización. Finalmente, se define un rango específico del eje horizontal ``(xlim(5000, 15000))`` para observar un segmento concreto de la señal filtrada. El comando ``plt.show()`` muestra la gráfica completa en pantalla.

```python
signal_filtrada = IIR_HP(signal)
signal_filtrada = IIR_LP(signal_filtrada)

plt.figure(figsize=(12, 6))
plt.plot(signal_filtrada)
plt.title('Señal ECG Filtrada')
plt.xlabel('Muestras (n)')
plt.ylabel('Amplitud (V)')
plt.grid(True)
plt.xlim(5000, 15000)
plt.show()
```
<p align="center">
<img width="70%" height="547" alt="image" src="https://github.com/user-attachments/assets/f4c0658d-7e6b-4a26-a68f-d3a300190068" />
</p>

### 4. Segmentación de la señal

Luego de que se aplica el filtrado digital para eliminar el ruido y tener más información útil, se realiza la segmentación en dos partes para poder realizar su análisis. Esta división permite observar como cambia la señal a medida que va avanzando el tiempo y las condiciones van cambiando. La señal completa, con una duración de 4 minutos, se divide en dos etapas: 

* La primera etapa: De 0 a 2 minutos, donde la persona se encuentra inmovil y en silencio total.
* La segunda etapa: De 2 a 4 minutos, la persona comienza a leer para estos ultimos minutos. 

La segmentación se realizo a partir del siguiente código:

> ### División de la señal

La señal toma 5000 muestras por segundo definida por $f_s$. A partir de esto, se define la duración de cada segmento en segundos para poder realizar el cálculo de cuántas muestras se tomaran para cada segmento. Esto se obtiene realizando la multiplicación de la duración del segmento por la cantidad de muestras por segundo. Luego se divide la señal, tomando las primeras 600k mmuestras para generar el primer segmento y las siguientes 600k muestras para el segmento 2. Finalmente, se crea el eje en el tiempo donde se genera un vector de 0 hasta 120 segundos y otro de 120 a 240 segundos. 

```python
fs = 5000
# 1. Dividir la señal en dos segmentos de 2 minutos cada uno
duracion_segmento = 2 * 60  # 2 minutos en segundos
muestras_segmento = int(duracion_segmento * fs)

segmento1 = signal_filtrada[:muestras_segmento]
segmento2 = signal_filtrada[muestras_segmento:2*muestras_segmento]

t1 = np.arange(len(segmento1)) / fs
t2 = np.arange(len(segmento2)) / fs + duracion_segmento
```

> ### Detección de los picos R-R

Primero se define una función llamada ``detectar_picos``, donde se decide qué valores son lo suficientemente grandes para que se consideren como un latido a partir de un valor de referencia que se acerque a los valores más altos de la señal, para que los picos R sean tomados en cuenta e ignore pequeñas subidas. Luego se da un tiempo minimo entre cada pico ya que no es comun que se den picos R en menos de 0.4s. Se calcula el tiempo entre cada pico R-R, para saber cada cuánto tarda un pico entre otro y se genera una nueva señal marcando donde se generan los picos para poder observarlos. Ya finalmente se detecta los picos para cada segmento de la señal.

```python
# 2. Función para detectar picos R 
def detectar_picos(ecg_segmento, fs):
    # Umbral dinámico basado en percentil alto para evitar picos chiquitos
    altura_min = np.percentile(ecg_segmento, 90)

    # Distancia mínima entre picos (ej. 0.4 s)
    distancia_min = int(0.4 * fs)

    # Detectar picos
    picos, propiedades = find_peaks(ecg_segmento, height=altura_min, distance=distancia_min)

    rr_intervals = np.diff(picos) / fs

    señal_picos = np.zeros_like(ecg_segmento)
    señal_picos[picos] = 1

    return picos, rr_intervals, señal_picos

# 3. Detectar picos en ambos segmentos
picos1, rr1, señal_picos1 = detectar_picos(segmento1, fs)
picos2, rr2, señal_picos2 = detectar_picos(segmento2, fs)
```

> ### Gráfica de segmentación

Se realiza el codigo para poder visualizar en la gráfica de cada segmento donde se generan los picos.

```python
# Graficar resultados
plt.figure(figsize=(15,8))

plt.subplot(2,1,1)
plt.plot(t1, segmento1, label='ECG Filtrada')
plt.plot(t1[picos1], segmento1[picos1], 'ro', label='Picos R')
plt.title("Segmento 1 (0 a 2 minutos) - Picos R sin suavizar")
plt.xlabel("Tiempo (s)")
plt.ylabel("Amplitud")
plt.legend()
plt.grid()

plt.subplot(2,1,2)
plt.plot(t2, segmento2, label='ECG Filtrada')
plt.plot(t2[picos2], segmento2[picos2], 'ro', label='Picos R')
plt.title("Segmento 2 (2 a 4 minutos) - Picos R")
plt.xlabel("Tiempo (s)")
plt.ylabel("Amplitud")
plt.legend()
plt.grid()

plt.tight_layout()
plt.show()
```

<p align="center">
<img width="1000" height="530" alt="image" src="https://github.com/user-attachments/assets/66044b29-154e-4235-9c79-7a245bd7a85a" />
</p>

> ### Señal intervalos R-R en el tiempo

Se logra visualizar los intervalos R-R, para cada segmento del ECG, extrayendo los tiempos de los picos R usando los indices de los picos que se detectaron. Se calcula el tiempo centrado para cada intervalo R-R, promediando el tiempo de dos picos consecutivos y se muestra la gráfica para cada segmento. 

```python
# Tiempos de los picos
tp1 = t1[picos1]
tp2 = t2[picos2]

# Intervalos RR (ya calculados)
nueva_senal_rr1 = rr1
nueva_senal_rr2 = rr2

# Tiempos centrados de los intervalos RR
t_rr1 = (tp1[:-1] + tp1[1:]) / 2
t_rr2 = (tp2[:-1] + tp2[1:]) / 2

# Graficar
plt.figure(figsize=(12,4))
plt.plot(t_rr1, nueva_senal_rr1, '-o')
plt.title("Nueva señal: Intervalos R-R (Segmento 1)")
plt.xlabel("Tiempo (s)")
plt.ylabel("Intervalo RR (s)")
plt.grid()
plt.show()

plt.figure(figsize=(12,4))
plt.plot(t_rr2, nueva_senal_rr2, '-o')
plt.title("Nueva señal: Intervalos R-R (Segmento 2)")
plt.xlabel("Tiempo (s)")
plt.ylabel("Intervalo RR (s)")
plt.grid()
plt.show()
```

<p align="center">
<img width="1000" height="386" alt="image" src="https://github.com/user-attachments/assets/dbb779b3-43c3-483c-9028-f0dd6dbdb9f4" />
<img width="1000" height="393" alt="image" src="https://github.com/user-attachments/assets/ed90441b-bb8b-4e87-a31a-383aa6fc798a" />
</p>

## d. Análisis de la HRV en el dominio del tiempo 

El análisis de la variabilidad de la frecuencia cardíaca, se centra en estudiar las variaciones que ocurren en los intervalos R-R que se dan en el electrocardiograma (ECG). Midiendo como cambia la duración entre cada latido cardíaco a lo largo del tiempo, a partir de estos intervalos R-R se calculan diferentes estadisticos que logran describir la dispersion o cambios, entres estos se encuetran la media reflejando el ritmo cardíaco promedio; la desviación estandar que representa la variabilidad total.

> ### Cálculos

Se realiza el análisis calculando la media de los intervalos R-R y su desviación estadandar a partir de las funciones ``np.mean`` ``np.std`` para cada segmento, se muestran los resultados y se realiza una comparación por medio de la diferencia de la media y desviación estandar entre los R-R de cada segmentos. Se gráfica la comparación permitiendo visualizar cómo várian los intervalos en los latidos.

```python
media_rr1 = np.mean(rr1)
media_rr2 = np.mean(rr2)

sd_rr1 = np.std(rr1, ddof=1)
sd_rr2 = np.std(rr2, ddof=1)

print("===== ANÁLISIS DE HRV - DOMINIO DEL TIEMPO =====\n")

print("Segmento 1 (0–2 min)")
print(f"Media RR = {media_rr1:.4f} s")
print(f"Desviación estándar RR = {sd_rr1:.4f} s")

print("\nSegmento 2 (2–4 min)")
print(f"Media RR = {media_rr2:.4f} s")
print(f"Desviación estándar RR = {sd_rr2:.4f} s")

# Comparación
print("\n===== COMPARACIÓN ENTRE SEGMENTOS =====")
print(f"Diferencia en media RR = {media_rr2 - media_rr1:.4f} s")
print(f"Diferencia en SD RR   = {sd_rr2 - sd_rr1:.4f} s")

plt.figure(figsize=(12,5))
plt.plot(rr1, label="RR Segmento 1", color='steelblue')
plt.plot(rr2, label="RR Segmento 2", color='purple')
plt.title("Series de Intervalos RR – Comparación")
plt.xlabel("Latido")
plt.ylabel("Intervalo RR (s)")
plt.legend()
plt.grid()
plt.show()
```

> ### Resultados y Gráfica

<p align="center"><b>Resultados</b></p>

<div align="center">
<pre>
===== ANÁLISIS DE HRV - DOMINIO DEL TIEMPO =====

Segmento 1 (0–2 min)
Media RR = 0.6670 s
Desviación estándar RR = 0.0377 s

Segmento 2 (2–4 min)
Media RR = 0.5787 s
Desviación estándar RR = 0.0684 s

===== COMPARACIÓN ENTRE SEGMENTOS =====
Diferencia en media RR = -0.0883 s
Diferencia en SD RR   = 0.0307 s
</pre>
</div>

<p align="center">
<img width="1000" height="471" alt="image" src="https://github.com/user-attachments/assets/bbac8392-38ab-4af2-8e40-4f7680c46a19" />
</p>

> ### Frecuencia cardíaca

<p align="center">
Segmento 1:

$$F_c=\frac{60}{media}$$

$$F_c=\frac{60}{0.667s}=90lpm$$
</p>

<p align="center">
Segmento 2:

$$F_c=\frac{60}{media}$$

$$F_c=\frac{60}{0.5787s}=103lpm$$
</p>

> ### Gráficos de Barras

<p align="center">
<img width="457" height="450" alt="image" src="https://github.com/user-attachments/assets/5aeeadea-18ce-4a94-9d8d-888789da9996" />
<img width="466" height="450" alt="image" src="https://github.com/user-attachments/assets/4c9f9505-9b23-477b-a247-9fb44d80890c" />
</p>

> ### Análisis

Para el primmer segmento (0 a 2 minutos), donde la persona se encontraba completamente inmovil y en completo silencio el intervalo R-R promedio fue de 0.667s, equivalente a una frecuencia cardíaca de 90lpm, junto con una desviación estandar de 0.0377s. Estos valores representan el estado "relajado" donde el sistema parasimpatico domina. Debido a que estar inmovil y en silencio reduce la necesidad de un gasto energético, manteniendo unaa frecuencia cardíaca estable, se puede observar una variabilidad estable reflejando el equilibrio en condiciones tranquilas.

En el segundo segmento (2 a 4 minutos), la persona se encontraba leyendo, la media del intervalo R-R ppromedio disminuye a un valor 0.5787s, equivalente a una frecuencia prommedio de 103lpm teniendo una actividad fisiologica mayor. La lectura no involucra como tal un esfuerzo físico, si incrementa una actividad simpatica debido a que requiere atención, coordinación y procesamiento cognitivo. La desviación estandar aumenta a un valor de 0.0684s, logrando observar una variabilidad más alta esto se puede dar por cambios en la respiración o movimiento que se dan al hablar.

En la comparación, se puede observar el paso del estado de reposo a un estado de mayor actividad simpatica.

# **Parte C**

## e. Diagrama de Poincare

Se realiza el diagrama de Poincare como otro metodo de observar la variabilidad de los picos R-R pero de una manera más directa, ayudando a observar si el corazón tiene o sigue un patron estable o si existen irregularidades que puedan sugerir arritmias.

> ## Programácion

Se realiza el diagrama a partir de la definición de una función ``poincare_plot`` que toma la serie de intervalos R-R. Dentro de la función, se crean dos arreglos: ``rr_n``, que contiene todos los intervalos R_R a excepción del último, y ``rr_n1``, que contiene todos a excepción del primero, de manera que cada punto ``(RR(n), RR(n+1))`` represente un intervalo consecutivo y el que le sigue. Luego se realiza visualización donde cada punto corresponde a un par de intervalos consecutivos, se agrega una línea diagonal ayudando como referencia, mostrando dónde se encontrarian los puntos si todos los intervalos fueran iguales. Finalmente, se llama a la función para ambos segmentos.

```python

def poincare_plot(rr, title): 
  rr_n = rr[:-1] # RR(n) 
  rr_n1 = rr[1:] # RR(n+1) 
  plt.figure(figsize=(6,6)) 
  plt.scatter(rr_n, rr_n1, s=20) 
  # Línea diagonal 
  minimo = min(rr_n.min(), rr_n1.min()) 
  maximo = max(rr_n.max(), rr_n1.max()) 
  plt.plot([minimo, maximo], [minimo, maximo], 'k-', linewidth=1) 
  plt.xlabel('RR(n) [s]')
  plt.ylabel('RR(n+1) [s]') 
  plt.title(title) 
  plt.grid(True) 
  plt.axis('equal') 
  plt.show() 
  
poincare_plot(rr1, "Poincaré - Segmento 1 (0–2 min)") 
poincare_plot(rr2, "Poincaré - Segmento 2 (2–4 min)")
```

> ## Cálculos SD1 y SD2 

Primero se calcula la diferencia y la suma entre los latidos consecutivos ``rr_n1, rr_n``, normalizandolo por $\sqrt{2}$, para que se quede sobre la linea de tendencia. Luego a cada uno de estos valores se les calcula la desviación estandar.

$$diff=\frac{rr_n1 - rr_n}{\sqrt{2}}$$

$$summ=\frac{rr_n1 + rr_n}{\sqrt{2}}$$

$$SD1=np.std(diff)$$

$$SD2=np.std(summ)$$

> ## Programación Elipse
Para la otra programación se realiza la misma definicion de laa función para el diagrama de pincare, sin embargo, se le agrega la representacion de la elipse para SD1 y SD2, utilizando las mismas funciónes y definiciones anteriores.Se calculan los valores de SD1 y SD2 y se agrega una elipse con rotación de 45° alrededor del centro de los datos ``(mean_rr_n, mean_rr_n_1)`` para representar gráficamente estas desviaciones, con la ayuda de una matriz de rotación que es importante debido a que deja la elipse centrada respecto a linea de identidad.

```python
def poincare_plot(rr, title):
    rr_n = rr[:-1]      
    rr_n1 = rr[1:]      

    # --- Calcular SD1 y SD2 ---
    diff = (rr_n1 - rr_n) / np.sqrt(2)
    summ = (rr_n1 + rr_n) / np.sqrt(2)

    SD1 = np.std(diff)
    SD2 = np.std(summ)

    # Centro de la elipse
    mean_rr_n  = np.mean(rr_n)
    mean_rr_n1 = np.mean(rr_n1)

    # --- Generar elipse SD1–SD2 ---
    theta = np.linspace(0, 2*np.pi, 200)
    ellipse_x = SD2 * np.cos(theta)
    ellipse_y = SD1 * np.sin(theta)

    # Rotación 45°
    R = np.array([[np.sqrt(0.5), -np.sqrt(0.5)],
                  [np.sqrt(0.5),  np.sqrt(0.5)]])
    ellipse_rot = R @ np.vstack([ellipse_x, ellipse_y])

    # --- Gráfico ---
    plt.figure(figsize=(6,6))
    plt.scatter(rr_n, rr_n1, s=10, alpha=0.3)

    # Línea identidad
    minimo = min(rr_n.min(), rr_n1.min())
    maximo = max(rr_n.max(), rr_n1.max())
    plt.plot([minimo, maximo], [minimo, maximo], 'k--', linewidth=1)

    # Elipse
    plt.plot(ellipse_rot[0] + mean_rr_n,
             ellipse_rot[1] + mean_rr_n1,
             'k', linewidth=2)

    plt.xlabel('RR(n) [s]')
    plt.ylabel('RR(n+1) [s]')
    plt.title(title + f"\nSD1 = {SD1:.4f}   SD2 = {SD2:.4f}")
    plt.grid(True)
    plt.axis('equal')
    plt.show()

poincare_plot(rr1, "Poincaré - Segmento 1 (0–2 min)")
poincare_plot(rr2, "Poincaré - Segmento 2 (2–4 min)")
```
> ## Gráficas

Se realizan dos tipos de diagramas de poincare, al realizar solo la nube de puntos en los primeros diagramas se logra observar la dinamica solo de los R-R, se puede observar si es estable, dispersa o irregular y también lograr visualizar el patron de la nuber. Cuando se realiza el diagrama de poincare con la elipse, esto ya permite calcular la variabilidad a un corto plazo y a largo; convirtiendo esto en una medida que se puede interpretar de manera fisiologica.

<p align="center"><b>Poincare sin elipse</b></p>

<p align="center">
<img width="504" height="500" alt="image" src="https://github.com/user-attachments/assets/32c85284-b0de-46f8-a26f-9f8d5c7e5011" />
<img width="492" height="500" alt="image" src="https://github.com/user-attachments/assets/2c492cac-0805-4669-9c88-5926800e5268" />
</p>

<p align="center"><b>Poincare con Elipse</b></p>

<p align="center">
<img width="487" height="500" alt="image" src="https://github.com/user-attachments/assets/9fcd63eb-07db-40a0-8109-1c232e81a884" />
<img width="475" height="500" alt="image" src="https://github.com/user-attachments/assets/69417da2-9622-45aa-878f-f4e62b7898bc" />
</p>

> ## Cálculos índices de actividad vagal (CVI) y de actividad simpática (CSI)

Luego de que se obtienen las variabilidades a largo y corto plazo y los diagramas de Poincare, se pueden calcular los indices de actividad vagal y simpática estimando como actua el sistema nervioso autónomo regula el corazón.

<p align="center"><b>Fórmula actividad vagal</b></p>

$$CVI=log(SD1*SD2)$$

<p align="center"><b>Fórmula actividad simpática</b></p>

$$CSI=\frac{SD2}{SD1}$$

> ### Programación

```python
def csi_cvi_from_rr(rr):
    SD1, SD2 = sd1_sd2_from_rr(rr)
    CSI = SD2 / SD1          # actividad simpática
    CVI = np.log10(SD1 * SD2)  # actividad vagal
    return CSI, CVI, SD1, SD2

CSI1, CVI1, SD1_1, SD2_1 = csi_cvi_from_rr(rr1)
CSI2, CVI2, SD1_2, SD2_2 = csi_cvi_from_rr(rr2)

print("Segmento 1:")
print(f"SD1 = {SD1_1:.4f} s, SD2 = {SD2_1:.4f} s")
print(f"CSI = {CSI1:.3f}, CVI = {CVI1:.3f}\n")

print("Segmento 2:")
print(f"SD1 = {SD1_2:.4f} s, SD2 = {SD2_2:.4f} s")
print(f"CSI = {CSI2:.3f}, CVI = {CVI2:.3f}\n")
```

> ### Resultados Índices

<p align="center"><b>Resultados</b></p>

<div align="center">
<pre>
Segmento 1:
SD1 = 0.0211 s, SD2 = 0.0490 s
CSI = 2.315, CVI = -2.985

Segmento 2:
SD1 = 0.0589 s, SD2 = 0.0767 s
CSI = 1.301, CVI = -2.345
</pre>
</div>

> ### Gráficos Barras

<p align="center">
<img width="430" height="300" alt="image" src="https://github.com/user-attachments/assets/86e75e7e-8077-475e-857b-86d065562a30" />
<img width="454" height="300" alt="image" src="https://github.com/user-attachments/assets/65e29c6c-c4e0-4223-916e-1d910aa9979e" />
</p>

> ## Análisis

Para los diagramas de poincare del segmento 1 se puede observar que los intervalos R-R presentan una distribución relativamente compacta alrededor de la línea de tendencia, donde la mayoria de intervalos consecutivos mantienen valores similares, reflejando un ritmo cardiaco estable durante este periodo. El rango de variación de los intervalos es estrecho, lo que sugiere que los cambios entre un latido y el siguiente son moderados concordando con los valores obtenidos para SD1=0.0211 y SD2=0.0480, mostrando una elipse alargada y delgada. A esto se agregan los resultados de los índices CSI = 2.276 y CVI = –2.995, los cuales indican, respectivamente, un predominio del componente longitudinal sobre el transversal (relacionado con un patrón más lineal y estable) y una baja complejidad en la dinámica de la serie R_R todo esto corresponde a la condición en la que se encontraba la persona donde no habia una actividad física.

Por otro lado, para el diagrama correspondiente al segmento 2 se observa una dispersión mayor en los puntos. Por lo que los intervalos R_R muestran más variabilidad y se alejan con mayor frecuencia de la línea de tendencia, lo que evidencia cambios más irregulares en la duración de los intervalos. El rango es más amplio en comparación al segmento 1 y aparecen puntos más distantes de la nube principal, indicando mayor irregularidad en la dinámica cardíaca durante este periodo. Este comportamiento coincide con el incremento significativo de las variaciones a largo y corto plazo SD1 = 0.0588s y SD2 = 0.0763s, las cuales generan una elipse más amplia y redondeada, señalando una mayor variación en los intervalos. Además, los índices CSI = 1.297 y CVI = –2.348 muestran un descenso en la relación longitudinal/transversal y un aumento en la frecuencia cardiaca respecto al primer segmento. Esto sugiere una modulación por el sistema nervioso simpatico-

Al comparar ambos segmentos, el primero muestra una señal completamente más estable y con menor variabilidad en los intervalos que el segundo segmento. Mientras que en los primeros dos minutos la dinámica de los intervalos R-R parece más controlada y consistente, en los minutos dos a cuatro la dispersión aumenta, lo que indica que el ritmo cardíaco se vuelve más variable. Esta transición también se refleja en los índices cuantitativos: tanto SD1 como SD2 aumentan notablemente en el segundo segmento, al igual que CVI, lo que sugiere mayor activida cardíaca. El CSI disminuye en el segundo segmento, indicando una reducción en la linealidad del patrón y una mayor influencia del componente transversal, asociado a un incremento de la variabilidad instantánea. Todo esto se da por las condiciones que se tenian en cada segmento.

# **Conclusiones**

Los resultados permiten inferir que la toma del ECG pasa de un estado inicial de estabilidad a uno de mayor variabilidad y adaptabilidad a medida que avanzó el registro. Esta transición puede asociarse a cambios fisiológicos, respiratorios o de movimiento que influye sobre la regulación autónoma del ritmo cardiaco. La combinación de los distintos análisis o pre análisis como lo fue el filtrado, segmentación temporal, media, desviación estandar, diagramas de Poincaré e índices cuantitativos como SD1, SD2, CSI y CVI permite tener una visualización más completa y profunda del comportamiento del ECG en diferentes condiciones. Cada herramienta logra dar más información el filtrado garantiza que se pueda observar la señal de mejor mánera y sin menos ruido, la segmentación permite estudiar la evolución temporal de la variabilidad en los diferentes tiempos que se tomaron, el diagrama de Poincaré ofrece una representación del comportamiento de los intervalos RR y los índices derivados cuantifican de manera precisa la magnitud y la complejidad de esa variabilidad. Gracias a esto, no solo es posible identificar cambios en el control autonómico, sino también interpretar cómo responde el organismo ante estímulos o diferentes condiciones. Por lo que, estos análisis resultan importantes para comprender la frecuencia cardíaca de manera completa en el estudio de la variabilidad del ritmo cardiaco.

> ## Notebook

**Link:** [Práctica 5 - HRV](https://colab.research.google.com/drive/18TmUIrqiQlBujNmEQrpMxll8Lo2TJ2vl?usp=sharing)
