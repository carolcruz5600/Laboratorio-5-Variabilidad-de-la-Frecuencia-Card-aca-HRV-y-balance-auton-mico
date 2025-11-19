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

# **Parte B**

> ### Cálculo manual de Filtro LP IIR

<p align="center">
<img width="769" height="1000" alt="image" src="https://github.com/user-attachments/assets/6423881f-adea-4be6-a9ec-c904c2600804" />
</p>

# **Parte C**
