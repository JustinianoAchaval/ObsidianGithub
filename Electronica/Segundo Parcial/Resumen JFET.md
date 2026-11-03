# Resumen Teórico: Transistores JFET (*Junction Field Effect Transistor*)

Este documento resume los fundamentos teóricos sobre el transistor JFET basados en la lección de **Electrónica FP**, abarcando su principio de funcionamiento, estructura física, curvas características, regiones operativas y comparativa frente a transistores bipolares.

---

## 1. ¿Qué es un JFET?

El **JFET** (*Transistor de Efecto de Campo por Unión*) es un dispositivo semiconductor de tres terminales perteneciente a la familia de los transistores de efecto de campo (FET). 

A diferencia de los transistores bipolares (BJT), el JFET es un dispositivo **unipolar**:
* La conducción de corriente se debe exclusivamente a un solo tipo de portadores mayoritarios (electrones en el canal N o huecos en el canal P).
* Es un dispositivo **controlado por tensión**: la corriente de salida ($I_D$) se modula mediante el voltaje aplicado a la entrada ($V_{GS}$).

---

## 2. Terminales y Estructura Física

Un JFET consta de una barra semiconductora dopada (que conforma el canal) y regiones fuertemente dopadas de tipo opuesto a los lados.

### Terminales
1. **Drenador ($D$ - *Drain*):** Terminal por el cual los portadores salen del canal.
2. **Fuente ($S$ - *Source*):** Terminal por el cual los portadores entran al canal.
3. **Puerta ($G$ - *Gate*):** Terminal de control que modula la sección efectiva del canal conductor.

### Tipos de Canal
* **Canal N:** El canal está formado por silicio tipo N (portadores mayoritarios: electrones). En la puerta hay regiones tipo P.
* **Canal P:** El canal está formado por silicio tipo P (portadores mayoritarios: huecos). En la puerta hay regiones tipo N.

---

## 3. Principio Físico de Funcionamiento

1. **Polarización inversa de la unión:** La unión Puerta-Canal ($P-N$) siempre se hace trabajar polarizada en **inversa** (para canal N, $V_{GS} \le 0\text{ V}$).
2. **Zona de deplexión o empobrecimiento:** Al polarizarse en inversa, se ensancha la zona carente de portadores libres alrededor de la unión.
3. **Control del canal:** Al hacer $V_{GS}$ más negativo, la zona de deplexión penetra más en el canal, estrechándolo y aumentando su resistencia interna, lo que restringe el paso de corriente $I_D$ entre Drenador y Fuente.
4. **Impedancia de entrada:** Dado que la unión se polariza en sentido inverso, la corriente de puerta es prácticamente nula ($I_G \approx 0\text{ A}$), lo que otorga al JFET una impedancia de entrada sumamente elevada (del orden de $10^8\ \Omega$ a $10^{12}\ \Omega$).

---

## 4. Parámetros Clave del JFET

* **$I_{DSS}$ (*Drain-to-Source Saturation Current*):** Máxima corriente de drenador cuando la tensión puerta-fuente es nula ($V_{GS} = 0\text{ V}$) y el dispositivo opera en saturación.
* **$V_P$ o $V_{GS(off)}$ (*Pinch-off Voltage* / Tensión de estrangulamiento o corte):** Tensión $V_{GS}$ a la cual la zona de deplexión estrangula por completo el canal, anulando la corriente de drenador ($I_D \approx 0$). Para un canal N, $V_P < 0$; para un canal P, $V_P > 0$.
* **Transconductancia ($g_m$ o $y_{fs}$):** Variación de la corriente de drenador respecto a un cambio en la tensión puerta-fuente:
  $$g_m = \left. \frac{\Delta I_D}{\Delta V_{GS}} \right|_{V_{DS} = \text{cte}}$$

---

## 5. Regiones de Operación

En las curvas de salida ($I_D$ vs $V_{DS}$ para distintos valores de $V_{GS}$):

### 1. Zona Óhmica o Lineal ($V_{DS} < V_{GS} - V_P$)
* Para valores pequeños de $V_{DS}$, el canal actúa como una resistencia controlada por tensión.
* A mayor valor negativo de $V_{GS}$, mayor resistencia ofrece el canal.
* Aplicación principal: atenuadores controlados por tensión, potenciómetros electrónicos.

### 2. Zona de Saturación o Activa ($V_{DS} \ge V_{GS} - V_P$)
* El canal sufre estrangulamiento en el extremo cercano al drenador.
* La corriente $I_D$ se independiza sustancialmente de $V_{DS}$ y queda controlada exclusivamente por $V_{GS}$.
* Sigue la **Ecuación de Shockley**:
  $$I_D = I_{DSS} \left(1 - \frac{V_{GS}}{V_P}\right)^2$$
* Aplicación principal: amplificación de señales y fuentes de corriente constante.

### 3. Zona de Corte ($V_{GS} \le V_P$ para canal N)
* El canal está totalmente estrangulado en toda su longitud.
* $I_D = 0\text{ A}$. El transistor se comporta como un circuito abierto entre drenador y fuente.

### 4. Zona de Ruptura (*Breakdown*)
* Si $V_{DS}$ supera la tensión de ruptura de la unión ($BV_{DS}$), se produce avalancha y la corriente crece descontroladamente, pudiendo destruir el componente.

---

## 6. Cuadro Comparativo: JFET vs BJT

| Característica | Transistor BJT | Transistor JFET |
| :--- | :--- | :--- |
| **Principio de control** | Controlado por corriente ($I_B$) | Controlado por tensión ($V_{GS}$) |
| **Portadores** | Bipolar (electrones y huecos) | Unipolar (un solo tipo) |
| **Impedancia de entrada** | Media / Baja ($1\text{ k}\Omega - 100\text{ k}\Omega$) | Extremadamente alta ($> 10^8\ \Omega$) |
| **Relación E/S** | Lineal aproximada ($I_C = \beta I_B$) | Cuadrática ($I_D \propto V_{GS}^2$) |
| **Nivel de ruido** | Mayor | Menor (ideal para etapas de preamplificación) |
| **Consumo de entrada** | Consume corriente continua | Prácticamente nulo ($I_G \approx 0$) |

---

## 7. Configuraciones de Polarización Comunes

1. **Autopolarización (*Self-bias*):**
   * Emplea una resistencia en el terminal de fuente ($R_S$) para fijar $V_S > 0$. Con $V_G = 0\text{ V}$, se logra automáticamente un valor negativo $V_{GS} = -I_D R_S$ sin requerir dos fuentes de alimentación.
2. **Polarización por divisor de tensión:**
   * Utiliza dos resistencias conectadas a la fuente de alimentación para fijar una tensión $V_G > 0$ combinada con una resistencia $R_S$, aportando mayor estabilidad frente a la dispersión de parámetros del fabricante ($I_{DSS}$ y $V_P$).