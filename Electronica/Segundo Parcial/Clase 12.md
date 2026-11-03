# Resumen Clase Nº 12: Amplificadores Diferenciales, OpAmp, Realimentación, Osciladores y Filtros

**Materia:** Electrónica / Dispositivos Electrónicos  
**Institución:** UNC - FCEFyN  
**Contenido:** Amplificador Diferencial, Amplificador Operacional (OpAmp) y configuraciones básicas, Realimentación (lazo abierto y cerrado), Osciladores y Fundamentos de Filtros.

---

## 1. El Amplificador Diferencial

El amplificador diferencial constituye la etapa de entrada elemental de la mayoría de los amplificadores integrados modernos y de los amplificadores operacionales (OpAmp).

### 1.1 Principio de Operación
* Posee dos terminales de entrada independientes: la entrada no inversora ($v_1$ o $v^+$) y la entrada inversora ($v_2$ o $v^-$).
* **Condición de salida:** Solo entrega tensión a la salida si existe una diferencia neta de potencial entre sus entradas:
  $$v_d = v_1 - v_2$$
* Si ambas entradas reciben la misma señal ($v_1 = v_2 \implies v_d = 0$), la salida idealmente es nula.

### 1.2 Ganancia Diferencial y Ganancia en Modo Común
Toda señal de entrada puede descomponerse en una componente diferencial ($v_d$) y una componente de modo común ($v_c$):
$$v_d = v_1 - v_2$$
$$v_c = \frac{v_1 + v_2}{2}$$

La tensión de salida real se modela como:
$$v_o = A_d v_d + A_c v_c$$

* **$A_d$ (Ganancia Diferencial):** Ganancia asociada a la resta de señales ($A_d \gg 1$).
* **$A_c$ (Ganancia en Modo Común):** Ganancia asociada a señales indeseadas idénticas presentes en ambas entradas (ruido de línea, zumbido de $50\text{ Hz}$). Idealmente $A_c = 0$.

### 1.3 Relación de Rechazo al Modo Común (CMRR)
Mide la capacidad del circuito para rechazar señales idénticas en ambas terminales frente a las diferenciales:
$$\text{CMRR} = \left|\frac{A_d}{A_c}\right|$$
$$\text{CMRR}_{[\text{dB}]} = 20 \log_{10}\left(\left|\frac{A_d}{A_c}\right|\right)$$
*En un amplificador diferencial de alta calidad, el $\text{CMRR}$ supera habitualmente los $80\text{ a }100\text{ dB}$.*

---

## 2. El Amplificador Operacional (OpAmp)

Es un circuito integrado analógico de acoplamiento directo, con amplificación diferencial interna y salida referenciada a tierra.

### 2.1 Modelo y Parámetros Ideales vs. Prácticos

| Parámetro | Símbolo | OpAmp Ideal | OpAmp Típico (ej. $\mu\text{A}741$) |
| :--- | :---: | :---: | :---: |
| **Impedancia de entrada** | $Z_i$ ($R_i$) | $\infty\ \Omega$ | $2\text{ M}\Omega\text{ a }10\text{ M}\Omega$ (BJT) / $> 10^{12}\ \Omega$ (FET) |
| **Impedancia de salida** | $Z_o$ ($R_o$) | $0\ \Omega$ | $< 100\ \Omega$ (típicamente $75\ \Omega$) |
| **Ganancia a lazo abierto** | $A_{OL}$ | $\infty$ | $\approx 2 \cdot 10^5\text{ a }10^6$ ($> 100\text{ dB}$) |
| **Ancho de banda** | $BW$ | $\infty\text{ Hz}$ | $\approx 1\text{ MHz}$ (GBW / Ganancia Unitaria) |
| **Tensión de Offset de entrada** | $V_{OS}$ | $0\text{ V}$ | $1\text{ mV a }5\text{ mV}$ |
| **Corrientes de polarización** | $I_B$ | $0\text{ A}$ | $\approx 80\text{ nA}$ |

### 2.2 Principio del Cortocircuito Virtual
Cuando el OpAmp opera en zona lineal con **realimentación negativa**:
1. **$I^+ = I^- = 0\text{ A}$:** Debido a que $Z_i \to \infty$, ninguna corriente penetra a los terminales de entrada del integrado.
2. **$v^+ \approx v^-$:** Dado que $v_o = A_{OL}(v^+ - v^-)$ y $A_{OL} \to \infty$, para que la salida no sature contra las fuentes de alimentación ($\pm V_{CC}$), la diferencia de tensión entre terminales debe tender a cero:
   $$v_d = v^+ - v^- = \frac{v_o}{A_{OL}} \approx 0 \implies v^+ = v^-$$

---

## 3. Configuraciones Lineales Fundamentales

### 3.1 Amplificador Inversor
La señal se ingresa a través del resistor $R_1$ al terminal inversor ($-$), mientras el terminal no inversor ($+$) se fija a masa ($0\text{ V}$).
* Por cortocircuito virtual: $v^- = v^+ = 0\text{ V}$ (**Masa Virtual**).
* Corrientes por Kirchhoff en el nodo inversor:
  $$i_1 = \frac{v_i - 0}{R_1} = \frac{v_i}{R_1}$$
  $$i_f = \frac{0 - v_o}{R_f} = -\frac{v_o}{R_f}$$
* Como $I^- = 0 \implies i_1 = i_f$:
  $$\frac{v_i}{R_1} = -\frac{v_o}{R_f} \implies v_o = -\frac{R_f}{R_1} v_i$$
* **Ganancia de tensión:** $A_v = -\frac{R_f}{R_1}$ (con desfasaje de $180^\circ$).
* **Impedancia de entrada:** $Z_i = R_1$.

### 3.2 Amplificador No Inversor
La señal de entrada $v_i$ se aplica directamente al terminal ($+$).
* Por cortocircuito virtual: $v^- = v^+ = v_i$.
* Divisor de tensión formado por $R_1$ y $R_f$ en la salida:
  $$v^- = v_o \cdot \frac{R_1}{R_1 + R_f} = v_i$$
* Despejando $v_o$:
  $$v_o = \left(1 + \frac{R_f}{R_1}\right) v_i$$
* **Ganancia de tensión:** $A_v = 1 + \frac{R_f}{R_1}$ (no inversor, desfase de $0^\circ$).
* **Impedancia de entrada:** $Z_i \to \infty$ (extremadamente alta).

### 3.3 Seguidor de Tensión (*Buffer* o Amplificador de Acoplamiento)
Caso especial del amplificador no inversor con $R_f = 0$ (cortocircuito directo de salida a entrada inversora) y $R_1 \to \infty$.
* **Tensión de salida:**
  $$v_o = v_i$$
* **Ganancia:** $A_v = 1$.
* **Características:** $Z_i \to \infty$ y $Z_o \approx 0$.
* **Aplicación:** Adaptador de impedancias para aislar sensores de alta impedancia interna sin cargar el circuito y evitar atenuación de la señal útil.

### 3.4 Amplificador Sumador Inversor
Permite sumar múltiples entradas ponderadas independientemente:
* Con $n$ fuentes conectadas a través de resistencias $R_1, R_2, \dots, R_n$ al terminal inversor:
  $$i_1 + i_2 + \dots + i_n = i_f$$
  $$\frac{v_{i,1}}{R_1} + \frac{v_{i,2}}{R_2} + \dots + \frac{v_{i,n}}{R_n} = -\frac{v_o}{R_f}$$
* Tensión de salida general:
  $$v_o = -R_f \left(\frac{v_{i,1}}{R_1} + \frac{v_{i,2}}{R_2} + \dots + \frac{v_{i,n}}{R_n}\right)$$
* Si $R_1 = R_2 = \dots = R_n = R$:
  $$v_o = -\frac{R_f}{R}\sum_{k=1}^n v_{i,k}$$

### 3.5 Amplificador Restador (Diferencial con OpAmp)
Circuito de sustracción formado por cuatro resistencias ($R_1, R_2, R_3, R_4$):
* Tensión en terminal no inversor ($v^+$):
  $$v^+ = v_2 \cdot \frac{R_4}{R_3 + R_4}$$
* Por cortocircuito virtual: $v^- = v^+$.
* Por superposición y nodo en $v^-$:
  $$v_o = v_2 \left(\frac{R_4}{R_3 + R_4}\right)\left(1 + \frac{R_2}{R_1}\right) - v_1 \left(\frac{R_2}{R_1}\right)$$
* **Condición de balance diferencial:** Si $\frac{R_2}{R_1} = \frac{R_4}{R_3}$:
  $$v_o = \frac{R_2}{R_1} (v_2 - v_1)$$

---

## 4. Concepto de Realimentación

### 4.1 Lazo Abierto vs. Lazo Cerrado
* **Lazo Abierto:** No existe conexión entre la salida y la entrada. La ganancia es máxima ($A_{OL}$), pero sumamente inestable, dependiente de la temperatura y propensa a la saturación rápida.
* **Lazo Cerrado:** Parte de la señal de salida se recircula a la entrada. Si la señal se reinyecta en oposición de fase (al borne inversor), se denomina **realimentación negativa**.

### 4.2 Efectos de la Realimentación Negativa
1. **Estabilización de la ganancia:** La ganancia global pasa a depender únicamente de componentes pasivos externos ($R_f, R_1$), volviéndose insensible a las variaciones térmicas de los transistores internos.
2. **Ensanchamiento del Ancho de Banda ($BW$):**  
   Al reducirse la ganancia por un factor $(1 + \beta A)$, la frecuencia de corte superior se extiende proporcionalmente:
   $$BW_f = BW \cdot (1 + \beta A)$$
   *El producto Ganancia $\times$ Ancho de Banda (GBW) se mantiene constante.*
3. **Modificación de impedancias:** Incrementa $Z_{in}$ y disminuye $Z_{out}$ en topologías de tensión.
4. **Reducción de distorsión no lineal y ruido.**

---

## 5. Osciladores Basados en OpAmp

Un oscilador es un circuito autónomo que convierte energía de continua (fuente de alimentación) en una forma de onda periódica en corriente alterna sin necesidad de una excitación externa.

### 5.1 Criterio de Oscilación (Barkhausen)
Para mantener una oscilación periódica sostenida en lazo cerrado:
1. El módulo de la ganancia de lazo debe ser unitario:
   $$|A \cdot \beta| = 1$$
2. El desfasaje neto total alrededor del lazo debe ser de $0^\circ$ o múltiplo de $360^\circ$:
   $$\angle(A \cdot \beta) = 0^\circ \quad (\text{o } 2\pi k)$$

### 5.2 Osciladores de Relajación (Generador de Onda Cuadrada)
* Utilizan un comparador con histeresis (realimentación positiva mediante divisor resistivo) combinado con una red de carga y descarga temporizada $R-C$ en el lazo inversor.
* **Comportamiento:** La tensión de salida conmuta de manera biestable entre los límites de saturación positiva y negativa ($\pm V_{sat}$), produciendo una señal cuadrada de periodo:
  $$T = 2 R C \ln\left(\frac{1 + \beta_{osc}}{1 - \beta_{osc}}\right) \quad \text{donde} \quad \beta_{osc} = \frac{R_1}{R_1 + R_2}$$

---

## 6. Introducción a Filtros de Señal

Un filtro es una red selectiva de frecuencia diseñada para transmitir libremente una banda espectral de interés (**banda de paso**) mientras rechaza o atenúa el resto de las frecuencias (**banda atenuada**).

### 6.1 Clasificación de Filtros Ideales

1. **Filtro Pasabajos (*Low-Pass*):** Permite el paso de frecuencias comprendidas entre $\omega = 0$ y la frecuencia de corte $\omega_c$. Atenúa completamente para $\omega > \omega_c$.
2. **Filtro Pasaaltos (*High-Pass*):** Atenúa frecuencias bajas ($0 \le \omega < \omega_c$) y transmite sin pérdidas a partir de $\omega \ge \omega_c$.
3. **Filtro Pasabanda (*Band-Pass*):** Conduce una banda intermedia delimitada entre una frecuencia inferior $\omega_1$ y una superior $\omega_2$ ($BW = \omega_2 - \omega_1$).
4. **Filtro Rechazabanda (*Notch* / *Band-Stop*):** Atenúa exclusivamente la ventana de frecuencias ubicada entre $\omega_1$ y $\omega_2$, permitiendo el paso por fuera de esos límites.

### 6.2 Filtros Ideales vs. Prácticos (Filtros Activos)
* **Filtros Ideales:** Poseen transiciones verticales instantáneas (pendiente infinita de atenuación) y respuesta perfectamente plana en banda de paso ($0\text{ dB}$). Son físicamente irrealizables (anticasuales).
* **Filtros Prácticos con OpAmps (Filtros Activos):**
  * Emplean elementos pasivos ($R, C$) combinados con un OpAmp como elemento activo.
  * **Ventajas:** No requieren inductores voluminosos, permiten obtener ganancia en la banda de paso y presentan alta impedancia de entrada y baja impedancia de salida.
  * **Limitación principal:** Están limitados por el producto Ganancia-Ancho de Banda (GBW) y el *Slew-Rate* del amplificador operacional, lo que suele restringir su uso a frecuencias por debajo de las centenas de kilohercios ($\approx\text{kHz}$).