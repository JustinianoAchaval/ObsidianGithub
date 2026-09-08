# Resumen Clase 5: Transistores Bipolares (BJT)

> **Nota personal:** Apunte completo de la Clase 5 sobre el BJT. Abarca desde la estructura física y la analogía hidráulica, hasta la polarización y el análisis de la recta de carga. 

---

## 1. Estructura y Operación del BJT

El transistor BJT (Bipolar Junction Transistor) amplía la estructura básica de la unión P-N del diodo y se presenta en dos tipologías: **PNP** y **NPN**[cite: 1].
*   **Terminales y dimensiones:** Posee Emisor (E), Base (B) y Colector (C)[cite: 1]. Físicamente, existe una asimetría de tamaño típica entre las regiones donde $a \approx 3,5\text{mm}$ y $b \approx 0,025\text{mm}$, resultando en una relación $a/b \approx 150$[cite: 1].
*   **Polarización de uniones:** Para que opere de forma normal, la unión Emisor-Base se polariza en directa, mientras que la unión Base-Colector se polariza en inversa (generando una región de empobrecimiento ancha en el colector)[cite: 1].
*   **Analogía Hidráulica:** Se puede comprender fácilmente su funcionamiento comparando la corriente eléctrica con un caudal de agua y la tensión con la presión[cite: 1]. El sistema actúa mediante compuertas mecánicas pivotantes donde una pequeña apertura (corriente de base) controla y habilita un flujo principal mucho mayor (corriente de colector)[cite: 1].

---

## 2. Regiones de Operación y Corrientes

El objetivo principal del BJT es implementar de manera eficiente el efecto de amplificación de señales[cite: 1]. Según cómo se lo polarice, su punto de operación (Punto Q) se establecerá en una de tres regiones[cite: 1]:
*   **Corte:** La unión C-E se comporta equivalente a una llave abierta ($I_B = 0$)[cite: 1].
*   **Saturación:** La unión C-E se comporta como una llave cerrada[cite: 1].
*   **Activa (Lineal):** El dispositivo no actúa como una simple llave de encendido/apagado, sino que amplifica linealmente las señales de entrada[cite: 1].
*   **Fórmulas de Corriente:** La corriente de colector es $\beta$ veces mayor que la corriente de base ($I_C = \beta I_B$), mientras que la corriente de emisor es aproximadamente igual a la del colector ($I_E \approx I_C$)[cite: 1].

---

## 3. Circuito de Polarización Fija

La polarización consiste en utilizar fuentes de corriente continua (CC) para fijar el punto de reposo $Q(V_{CEQ}, I_{CQ})$ en la región deseada antes de inyectar una pequeña señal[cite: 1].
*   **Ecuación Malla Base-Emisor:** 
    $$ I_B = \frac{V_{CC} - V_{BE}}{R_B} $$[cite: 1]
*   **Ecuación Malla Colector-Emisor:** 
    $$ V_{CE} = V_{CC} - I_C R_C $$[cite: 1]

---

## 4. Variaciones de la Recta de Carga

El Punto Q se desplaza sobre la recta de carga trazada en las curvas características de salida si se alteran los componentes del circuito[cite: 1]:
*   **Variación de $I_B$:** Si $I_B$ aumenta, el Punto Q se desplaza hacia arriba logrando mayor $I_C$, manteniendo estáticos los cortes en los ejes coordenados[cite: 1].
*   **Variación de $R_C$:** Una menor resistencia de colector cambia la pendiente de la recta, elevando el punto de corte máximo en el eje Y de corriente[cite: 1].
*   **Variación de $V_{CC}$:** Altera el corte en el eje X, desplazando toda la recta de forma paralela[cite: 1].