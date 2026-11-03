# Resumen Integral: Transistores de Efecto de Campo (JFET y MOSFET)
**Materia:** Electrónica / Dispositivos Electrónicos  
**Contenido:** Clases Nº 8, 9 y 10 (UNC - FCEFyN)

---

## 1. Introducción a los Transistores de Efecto de Campo (FET)

### 1.1 Definición y Diferencias Fundamentales con el BJT
* **Control por Tensión vs. Control por Corriente:** Mientras que el BJT es un dispositivo controlado por corriente en la base ($I_B$), el FET es un dispositivo controlado exclusivamente por el campo electrostático originado por una diferencia de potencial aplicada entre la compuerta y la fuente ($V_{GS}$).
* **Dispositivo Unipolar:** La corriente principal está transportada por un único tipo de portador mayoritario (electrones en canal N o huecos en canal P).
* **Impedancia de Entrada ($Z_{in}$):** Extremadamente alta ($10^9\,\Omega$ a $10^{14}\,\Omega$), haciendo que en continua la corriente de compuerta sea prácticamente nula:
  $$I_G \approx 0\text{ A}$$
* **Estabilidad Térmica:** Coeficiente de temperatura negativo a altas corrientes, lo cual previene el embalamiento térmico típico de los BJT.

### 1.2 Clasificación General
1. **JFET (*Junction Field-Effect Transistor*):** Unión PN polarizada en inversa.
2. **MOSFET (*Metal-Oxide-Semiconductor Field-Effect Transistor*):** Aislación por óxido de silicio ($\text{SiO}_2$).
   * **Tipo Empobrecimiento (*Depletion* / D-MOSFET):** Canal físico preexistente.
   * **Tipo Enriquecimiento (*Enhancement* / E-MOSFET):** Sin canal físico inicial; requiere inversión inducida por campo.
3. Subclasificación por portadores: **Canal N** y **Canal P**.

---

## 2. Transistor JFET (Clases 8 y 9)

### 2.1 Estructura Física y Terminales (Canal N)
* **Drenaje ($D$):** Terminal por donde egresan los electrones y entra la corriente de drenaje $I_D$.
* **Fuente ($S$):** Terminal por donde ingresan los electrones al canal.
* **Compuerta ($G$):** Terminales conectadas a regiones semiconductoras tipo P muy dopadas incrustadas en los laterales del canal N.
* **Región de empobrecimiento (*Depletion Region*):** Al no inyectar corriente directa ($V_{GS} \le 0\text{ V}$), la unión PN queda en inversa, creando una zona vacía de portadores que estrangula físicamente la sección transversal del canal.

### 2.2 Modos de Operación y Curvas Características
1. **Condición I ($V_{GS} = 0\text{ V}$, $V_{DS} > 0\text{ V}$):**  
   Al aumentar $V_{DS}$, circula una corriente $I_D$ de $D$ hacia $S$. Como la caída óhmica interna a lo largo del canal hace que la zona cercana a $D$ esté a mayor potencial respecto a $G$ que la zona de $S$, la zona de empobrecimiento es más ancha arriba que abajo (forma asimétrica).  
   Al llegar a $V_{DS} = -V_p$, se produce el **estrangulamiento (*pinch-off*)**, alcanzando la corriente de saturación máxima $I_{DSS}$.

2. **Condición II ($V_{GS} < 0\text{ V}$, $V_{DS} > 0\text{ V}$):**  
   Una tensión negativa en compuerta suma polarización inversa de base. El estrangulamiento ocurre a menores valores de $V_{DS}$ y la corriente máxima alcanzable disminuye progresivamente.

### 2.3 Regiones de Operación en las Curvas $I_D$ vs. $V_{DS}$
* **Región Óhmica (Lineal / Resistor controlado por tensión):**
  Para tensiones $V_{DS} < V_{DS,\text{sat}}$:
  $$r_d = \frac{r_o}{\left(1 - \frac{V_{GS}}{V_p}\right)^2} \quad \text{con} \quad r_o = -\frac{V_p}{I_{DSS}}$$
* **Región de Saturación (Activa para amplificación):**  
  El JFET se comporta como una fuente de corriente controlada por tensión ($V_{GS}$). Se rige por la **Ecuación de Shockley**:
  $$I_D = I_{DSS} \left(1 - \frac{V_{GS}}{V_p}\right)^2$$
  *Donde $V_p < 0\text{ V}$ para canal N, y $V_p > 0\text{ V}$ para canal P.*

* **Región de Ruptura (*Breakdown*):**  
  Para tensiones $V_{DS} \ge BV_{DSO}$, la unión entra en avalancha y la corriente sube abruptamente.

### 2.4 Puntos Notables de la Curva de Transferencia (Shockley)
| $V_{GS}$ | Corriente $I_D$ |
| :--- | :--- |
| $0\text{ V}$ | $I_{DSS}$ |
| $0{,}3 \cdot V_p$ | $\frac{I_{DSS}}{2}$ |
| $0{,}5 \cdot V_p$ | $\frac{I_{DSS}}{4}$ |
| $V_p$ | $0\text{ A}$ |

### 2.5 Límites de Operación Lineal
Para asegurar funcionamiento en régimen lineal seguro:
$$\begin{cases}
V_{DS} \ge V_{GS} - V_p \\
V_{DS} \le V_{DS,\max} \\
I_D \le I_{DSS} \\
P_D = V_{DS} \cdot I_D \le P_{\max}
\end{cases}$$

---

## 3. Transistores MOSFET (Clase 9)

### 3.1 Estructura General
La compuerta metálica está completamente aislada del canal semiconductor por una capa de dióxido de silicio ($\text{SiO}_2$), logrando una resistencia de entrada del orden de $10^{12}$ a $10^{15}\,\Omega$. El terminal de sustrato (*Substrate* o $SS$) usualmente se conecta internamente a la fuente ($S$).

### 3.2 MOSFET de Empobrecimiento (*Depletion* / D-MOSFET)
* **Principio:** Posee un canal físico semiconductor N difuminado de fábrica entre drenaje y fuente.
* **Modos de trabajo:**
  * **Modo Empobrecimiento ($V_{GS} < 0\text{ V}$):** Repele electrones del canal hacia el sustrato, reduciendo la conducción ($I_D < I_{DSS}$).
  * **Modo Enriquecimiento ($V_{GS} > 0\text{ V}$):** Atrae electrones adicionales al canal, permitiendo corrientes mayores que $I_{DSS}$.
* **Ecuación gobernante en saturación:** Ecuación de Shockley idéntica al JFET:
  $$I_D = I_{DSS}\left(1 - \frac{V_{GS}}{V_p}\right)^2$$

### 3.3 MOSFET de Enriquecimiento (*Enhancement* / E-MOSFET)
* **Principio:** No posee canal físico inicial. Drenaje y fuente son islas tipo N separadas por un sustrato tipo P continuo.
* **Voltaje Umbral ($V_T$ o $V_{GS(\text{th})}$):** Valor de tensión positiva mínima en compuerta requerida para repeler huecos del sustrato y atraer electrones, formando la **capa de inversión** (canal inducido).
* **Ecuaciones en saturación ($V_{GS} > V_T$ y $V_{DS} \ge V_{GS} - V_T$):**
  $$I_D = k \left(V_{GS} - V_T\right)^2$$
  Donde la constante constructiva $k$ se calcula a partir de datos de catálogo ($V_{GS(\text{on})}$, $I_{D(\text{on})}$):
  $$k = \frac{I_{D(\text{on})}}{\left(V_{GS(\text{on})} - V_T\right)^2}$$

---

## 4. Polarización en Corriente Continua (CC / Punto Q) (Clases 9 y 10)

### 4.1 Autopolarización del JFET (*Self-Bias*)
Circuito con resistencia de drenaje $R_D$, resistencia de fuente $R_S$ y resistencia de compuerta a masa $R_G$.

1. Como $I_G = 0 \implies V_{RG} = 0\text{ V} \implies V_G = 0\text{ V}$.
2. Potencial de fuente:
   $$V_S = I_D \cdot R_S$$
3. Malla de entrada:
   $$V_{GS} = V_G - V_S = -I_D \cdot R_S$$
4. Ecuación cuadrática para $I_{DQ}$ (intersección con Shockley):
   $$I_D = I_{DSS} \left(1 + \frac{I_D \cdot R_S}{V_p}\right)^2$$
   *Se resuelve por Bhaskara eligiendo la raíz dentro de los límites físicos ($0 \le I_{DQ} \le I_{DSS}$).*
5. Tensiones de reposo:
   $$V_{SQ} = I_{DQ} \cdot R_S$$
   $$V_{DQ} = V_{DD} - I_{DQ} \cdot R_D$$
   $$V_{DSQ} = V_{DQ} - V_{SQ} = V_{DD} - I_{DQ}(R_D + R_S)$$

### 4.2 Polarización por Divisor Resistivo de Tensión
Uso de divisor $R_1$ y $R_2$ en la compuerta alimentado por $V_{DD}$:
$$V_G = V_{DD} \cdot \frac{R_2}{R_1 + R_2}$$
$$V_{GS} = V_G - I_D \cdot R_S$$
Sustituyendo en la ecuación de Shockley se obtiene el punto de trabajo analítico o mediante la recta de carga de polarización en el gráfico de transferencia.

---

## 5. Modelo en Pequeña Señal y Análisis en Corriente Alterna (CA) (Clase 10)

### 5.1 Parámetro de Transconductancia ($g_m$)
Representa la ganancia intrínseca de conversión tensión a corriente del transistor:
$$g_m = \left.\frac{\partial I_D}{\partial V_{GS}}\right|_{Q}$$

* **Para JFET y D-MOSFET:**
  $$g_m = g_{m0}\left(1 - \frac{V_{GSQ}}{V_p}\right) \quad \text{donde} \quad g_{m0} = \frac{2 I_{DSS}}{|V_p|}$$
  En función de la corriente de drenaje de reposo:
  $$g_m = g_{m0}\sqrt{\frac{I_{DQ}}{I_{DSS}}}$$

* **Para E-MOSFET:**
  $$g_m = 2 k \left(V_{GSQ} - V_T\right) = 2\sqrt{k \cdot I_{DQ}}$$

### 5.2 Modelo Lineal de Parámetros de Dos Puertos (Cuadripolo)
* **Entrada:** Circuito abierto ($Z_{in} \to \infty$).
* **Salida:** Fuente de corriente dependiente $g_m \cdot v_{gs}$ en paralelo con la resistencia dinámica de salida $r_d$ (donde $r_d = \frac{1}{y_{os}} \approx \frac{V_A + V_{DS}}{I_D}$).

### 5.3 Configuraciones Básicas de Amplificadores con FET
| Configuración | Ganancia de Tensión ($A_v$) | Impedancia de Entrada ($Z_i$) | Impedancia de Salida ($Z_o$) |
| :--- | :--- | :--- | :--- |
| **Fuente Común con Autopolarización** ($R_S$ desacoplada con $C_S$) | $A_v = -g_m (R_D \parallel r_d)$ *(Inversor)* | $Z_i = R_G$ | $Z_o \approx R_D$ |
| **Fuente Común con $R_S$ sin desacoplar** | $A_v = \frac{-g_m (R_D \parallel r_d)}{1 + g_m R_S}$ | $Z_i = R_G$ | $Z_o \approx R_D$ |
| **Drenaje Común (Seguidor de Fuente)** | $A_v \approx \frac{g_m (R_S \parallel r_d)}{1 + g_m (R_S \parallel r_d)} \approx 1$ *(No inversor)* | $Z_i = R_G$ | $Z_o \approx R_S \parallel \frac{1}{g_m}$ *(Baja)* |

### 5.4 Efecto de la Resistencia Interna de Fuente ($R_s$) y la Carga ($R_L$)
* Con fuente no ideal ($v_i$ en serie con $R_s$):
  $$v_{gs} = v_i \cdot \frac{Z_i}{Z_i + R_s}$$
  Como $Z_i = R_G$ suele ser del orden de los Megaohms ($M\Omega$), prácticamente toda la tensión de entrada cae en la compuerta: $v_{gs} \approx v_i$.
* Con carga $R_L$ acoplada a la salida, $R_D$ se sustituye por la combinación en paralelo:
  $$R_L' = R_D \parallel R_L$$
  Lo que reduce la ganancia efectiva total:
  $$A_{vs} = \frac{v_o}{v_i} = -g_m \left(R_D \parallel R_L \parallel r_d\right) \cdot \frac{R_G}{R_G + R_s}$$