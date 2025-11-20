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

> ### Parte C

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

<img width="1001" height="547" alt="image" src="https://github.com/user-attachments/assets/1e9eeb0b-4596-4a89-b3d0-7f7230b64c8f" />

# **Parte B**
## c. Pre-procesamiento de la señal

Para garantizar una correcta interpretación de la señal electrocardiográfica (ECG), es necesario eliminar el ruido producido por el movimiento, la respiración y la deriva de la línea base. En este laboratorio se adquirió la señal ECG de un sujeto durante cuatro minutos: dos en reposo y dos leyendo en voz alta, verificando previamente que la frecuencia de muestreo y la cuantificación fueran adecuadas.

Posteriormente, se diseñaron e implementaron dos filtros digitales IIR: un filtro pasa-alto para corregir la deriva de baja frecuencia y un filtro pasa-banda para resaltar el contenido espectral propio del ECG. Finalmente, se obtuvo la ecuación en diferencias de cada filtro y se aplicaron a la señal asumiendo condiciones iniciales en cero.

### 1. Filtro HP IIR 

>### 1.1. Diseño del Filtro

>### Parámetros

En esta primera etapa se establecen los parámetros principales del filtro IIR pasa-altos. Se definen las frecuencias límite ``f₁ = 0.5 Hz`` y ``f₂ = 2 Hz``, que corresponden al inicio de la banda de rechazo y de la banda de transición, respectivamente. También se especifican las atenuaciones requeridas para cada banda, siendo ``k₁ = −10 dB`` en la banda de rechazo y ``k₂ = −3 dB`` en la banda de transición. 

Estos valores constituyen la base sobre la cual se calculará el orden del filtro y su comportamiento deseado en frecuencia.

<img width="885" height="660" alt="image" src="https://github.com/user-attachments/assets/8ffc071e-ce9f-49ea-b28f-c10796bc3f6d" />

>### Pasar a Requisitos Digitales

Luego se trasladan las frecuencias analógicas al dominio digital mediante la normalización con la frecuencia de muestreo, que en este caso es de ``5000 muestras por segundo``. A partir de esta conversión se obtienen las frecuencias digitales equivalentes ``ω₁ = 6.28×10⁻⁴ rad/muestra`` y ``ω₂ = 25.14×10⁻⁴ rad/muestra``. 

Estos valores permiten definir con precisión las bandas del filtro dentro del dominio discreto en el cual será implementado.


<img width="513" height="196" alt="image" src="https://github.com/user-attachments/assets/7394a8d7-46f5-4307-94db-dd68c7fe420d" />

>### T1 y Pre-Warping

Debido a la distorsión que introduce la transformación bilineal, se aplica el proceso de pre-warping con la expresión ``Ω = 2·tan(ω/2)``. Este procedimiento permite corregir las frecuencias digitales anteriores y obtener las versiones ajustadas ``Ω₁ = 6.28×10⁻⁴`` y ``Ω₂ = 25.14×10⁻⁴``. Estas frecuencias corregidas garantizan que, una vez realizada la transformación al dominio Z, el filtro digital mantenga las características especificadas en el diseño analógico original.

<img width="535" height="129" alt="image" src="https://github.com/user-attachments/assets/92541e15-077c-46ec-9700-7b8ad359dc20" />

>### Filtro Análogo

Con las frecuencias corregidas se determinan los valores normalizados ``Ωᵣ = 4 rad/s`` y ``Ωₚ = 1 rad/s``, que representan las fronteras de la banda de rechazo y la banda de paso en el diseño analógico. A partir de estos valores y de las atenuaciones definidas, se calcula que el filtro requerido es de primer orden. Posteriormente se obtiene la función de transferencia analógica correspondiente, la cual adopta la forma pasa-altos y constituye la base previa a la digitalización completa del filtro.

<img width="608" height="541" alt="image" src="https://github.com/user-attachments/assets/388bd74f-12ee-466f-ae74-422ae8540a46" />

>### Transformación Bilineal
Para llevar el filtro al dominio Z se reemplaza la variable analógica **s** por su forma bilineal equivalente: ``s = 2·(1 − z⁻¹) / (1 + z⁻¹)``. Tras esta sustitución y la correspondiente simplificación algebraica, se obtiene una expresión discreta de la función de transferencia. En este desarrollo aparecen coeficientes numéricos relevantes como ``2.002514`` y ``1.997486``, así como términos dependientes de ``z⁻¹``, que permiten identificar y extraer directamente los coeficientes finales del filtro digital.

<img width="798" height="327" alt="image" src="https://github.com/user-attachments/assets/527594f8-28be-4c12-9bd5-2978e902c54e" />

>### Ecuación en Diferencias

Finalmente, a partir de la función ``H(z)`` obtenida, se despeja la ecuación en diferencias que define cómo el filtro procesa cada muestra. La ecuación resultante es: ``y(n) = 0.998744·x(n) − 0.998744·x(n−1) + 0.997489·y(n−1)``. Los coeficientes ``0.998744`` y ``0.997489`` representan los valores exactos obtenidos en el cálculo del filtro. Esta relación recursiva describe cómo la salida actual depende tanto de las entradas actual y pasada como de la salida previa, finalizando así la implementación digital del filtro pasa-altos.

<img width="651" height="335" alt="image" src="https://github.com/user-attachments/assets/8a510ad4-f0c3-489e-b5e8-fb66751ddfc6" />

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

<img width="689" height="288" alt="image" src="https://github.com/user-attachments/assets/51fa572f-c955-4fcd-a14f-57ba9dcde36b" />

>### T1 y Pre-Warping

Se aplica la corrección por pre-warp usando la fórmula Ω=2tan(𝜔/2). A partir de los valores digitalizados, se obtienen frecuencias corregidas como Ω1=0.15 y Ω2=0.252	​, que compensan la distorsión generada por la transformación bilineal.

<img width="364" height="177" alt="image" src="https://github.com/user-attachments/assets/efe55343-760b-4a2c-bec5-673ec3d51dad" />

>### Filtro Análogo

Con las frecuencias corregidas se calcula el orden del filtro usando la expresión logarítmica, obteniéndose 𝑛=2. Luego se determina la función de transferencia analógica.

<img width="793" height="634" alt="image" src="https://github.com/user-attachments/assets/a7f67030-b79e-43b5-b664-0b8c04589ce8" />

>### Transformación Bilineal

En esta etapa se sustituye la variable s por su equivalente bilineal, definido como: s = 2(1 − z⁻¹) / (1 + z⁻¹). Esta transformación permite obtener la función de transferencia en el dominio Z. Durante el proceso aparecen coeficientes característicos del filtro digital, tales como 3.44×10⁻³, 1.032×10⁻² y 3.94×10⁻³, los cuales conforman los parámetros finales del filtro implementado.

<img width="1648" height="785" alt="image" src="https://github.com/user-attachments/assets/bafea7d0-4eb4-4958-a4c4-a3a204219492" />

>### Ecuación en Diferencias

Finalmente, a partir de la función H(z) se despeja la ecuación en diferencias que implementa el filtro. En esta expresión aparecen coeficientes característicos como 3.304, -7.118, 4.718 y -0.876, que multiplican las salidas anteriores ``y(n−1)``, ``y(n−2)`` y ``y(n−3)``. También se identifican los coeficientes asociados a las entradas: 3.44×10⁻³, 1.032×10⁻² y nuevamente 3.44×10⁻³. Esta ecuación describe cómo se obtiene cada nueva muestra del filtro FIR/LB a partir de combinaciones lineales de entradas y salidas previas.

<img width="1780" height="415" alt="image" src="https://github.com/user-attachments/assets/2518aa97-3490-493a-b6b2-062859ef7d6e" />

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

<img width="1012" height="547" alt="image" src="https://github.com/user-attachments/assets/f4c0658d-7e6b-4a26-a68f-d3a300190068" />

# **Parte C**
