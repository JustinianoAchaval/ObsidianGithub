# Resumen Clase Nº 11: Conexión Darlington, Decibelios y Respuesta en Frecuencia
**Materia:** Electrónica / Dispositivos Electrónicos  
**Institución:** UNC - FCEFyN  
**Contenido:** Par Darlington, Decibelios, Respuesta en Baja Frecuencia, Respuesta en Alta Frecuencia y Diagramas de Bode.

---

## 1. Conexión Darlington

La conexión Darlington es una configuración multietapa de dos transistores bipolares (BJT) conectados en cascada directa para operar como un único transistor equivalente de ganancia de corriente ultra alta.

### 1.1 Configuración y Conexión
* El emisor del primer transistor ($Q_1$) se conecta directamente a la base del segundo transistor ($Q_2$).
* Los colectores de ambos transistores se conectan en común ($C_1 = C_2 = C$).
* Terminales equivalentes:
  * **Base equivalente ($B$):** Base de $Q_1$.
  * **Colector equivalente ($C$):** Colectores unidos de $Q_1$ y $Q_2$.
  * **Emisor equivalente ($E$):** Emisor de $Q_2$.

### 1.2 Parámetros Principales
1. **Ganancia de Corriente ($\beta_D$):**
   $$i_{b2} = i_{e1} \approx \beta_1 i_{b1}$$
   $$i_c \approx i_{c2} \approx \beta_2 i_{b2} = \beta_2 (\beta_1 i_{b1})$$
   $$\beta_D \approx \beta_1 \cdot \beta_2$$

2. **Caída de Tensión Base-Emisor en Reposo ($V_{BE(D)}$):**
   $$V_{BE(D)} = V_{BE1} + V_{BE2} \approx 0{,}7\text{ V} + 0{,}7\text{ V} = 1{,}4\text{ V}$$

3. **Impedancia de Entrada ($Z_i$):**
   $$Z_i \approx \beta_1 \cdot \beta_2 \cdot R_E = \beta_D \cdot R_E$$
   *(Resulta sustancialmente más alta que la de una etapa de emisor común o seguidor simple).*

---

## 2. El Decibelio ($\text{dB}$) y Escalas Logarítmicas

El decibelio se utiliza para comprimir rangos dinámicos amplios de ganancia y frecuencia, y para convertir el producto de ganancias en cascada en una suma algebraica directa.

### 2.1 Propiedades del Logaritmo Decimal
* $x = \log_{10}(a) \iff 10^x = a$
* $\log_{10}(a \cdot b) = \log_{10}(a) + \log_{10}(b)$
* $\log_{10}\left(\frac{a}{b}\right) = \log_{10}(a) - \log_{10}(b)$
* $\log_{10}(a^n) = n \cdot \log_{10}(a)$
* $\log_{10}(1) = 0$

### 2.2 Definiciones de Ganancia en $\text{dB}$
* **Ganancia de Potencia:**
  $$G_P[\text{dB}] = 10 \log_{10}\left(\frac{P_o}{P_i}\right)$$

* **Ganancia de Tensión y Corriente:**
  $$G_v[\text{dB}] = 20 \log_{10}\left(\left|\frac{V_o}{V_i}\right|\right) = 20 \log_{10}(|A_v|)$$
  $$G_i[\text{dB}] = 20 \log_{10}\left(\left|\frac{I_o}{I_i}\right|\right)$$

### 2.3 Tabla de Valores Notables

| Relación $\frac{P_o}{P_i}$ (Potencia) | $G_P$ [$\text{dB}$] | Relación $\frac{V_o}{V_i}$ o $\frac{I_o}{I_i}$ (Tensión/Corriente) | $G_v$ [$\text{dB}$] |
| :---: | :---: | :---: | :---: |
| $0{,}5$ | $-3\text{ dB}$ (Punto de media potencia) | $0{,}5$ | $-6\text{ dB}$ |
| $0{,}707$ ($\frac{1}{\sqrt{2}}$) | $-1{,}5\text{ dB}$ | $0{,}707$ ($\frac{1}{\sqrt{2}}$) | $-3\text{ dB}$ (Frecuencia de corte) |
| $1$ | $0\text{ dB}$ | $1$ | $0\text{ dB}$ |
| $2$ | $+3\text{ dB}$ | $2$ | $+6\text{ dB}$ |
| $10$ | $+10\text{ dB}$ | $10$ | $+20\text{ dB}$ |
| $100$ | $+20\text{ dB}$ | $100$ | $+40\text{ dB}$ |

---

## 3. Concepto General de Respuesta en Frecuencia

* Las señales reales están formadas por múltiples armónicos y componentes de frecuencia (descomposición en series o transformada de Fourier).
* Un amplificador lineal no responde uniformemente en todo el espectro $0 \le f < \infty$.
* **Ancho de Banda ($BW$ o $AB$):**
  $$AB = f_{H} - f_{L}$$
  *Donde $f_L$ es la frecuencia de corte inferior y $f_H$ es la frecuencia de corte superior.*
* **Banda de Frecuencias Medias:** Región plana donde todos los condensadores de acoplo y desacoplo actúan como cortocircuitos ideales ($X_C \approx 0$) y las capacidades parásitas internas actúan como circuitos abiertos ($X_C \approx \infty$).

---

## 4. Respuesta en Baja Frecuencia (Amplificador BJT)

En bajas frecuencias, la reactancia de los condensadores externos ($X_C = \frac{1}{2\pi f C}$) aumenta, provocando caídas de señal y atenuación de la ganancia.

### 4.1 Frecuencias de Corte por Condensadores Externos

Para una etapa típica polarizada por divisor de tensión:

1. **Condensador de Acoplo de Entrada ($C_1$ o $C_i$):**
   Determinado por $C_1$, la resistencia interna del generador $R_{sig}$ y la impedancia de entrada $R_i$:
   $$R_i = R_1 \parallel R_2 \parallel (\beta r_e)$$
   $$f_{C1} = \frac{1}{2\pi (R_{sig} + R_i) C_1}$$

2. **Condensador de Acoplo de Salida ($C_2$ o $C_o$):**
   Determinado por $C_2$, la resistencia de salida del amplificador $R_o$ y la resistencia de carga $R_L$:
   $$R_o = R_C \parallel r_o \approx R_C$$
   $$f_{C2} = \frac{1}{2\pi (R_o + R_L) C_2}$$

3. **Condensador de Desacoplo de Emisor ($C_E$):**
   Determinado por la resistencia equivalente vista por el emisor ($R_e$):
   $$R'_S = R_{sig} \parallel R_1 \parallel R_2$$
   $$R_e = R_E \parallel \left(\frac{R'_S}{\beta} + r_e\right)$$
   $$f_{CE} = \frac{1}{2\pi R_e C_E}$$

### 4.2 Frecuencia de Corte Inferior Crítica ($f_L$)
La frecuencia de corte inferior efectiva del circuito la impone la **mayor** de las tres frecuencias calculadas:
$$f_L = \max(f_{C1},\, f_{C2},\, f_{CE})$$

### 4.3 Diagrama de Bode en Baja Frecuencia
* **Frecuencias medias ($f \gg f_L$):** Ganancia constante nominal $A_{v,\text{mid}}$:
  $$A_{v,\text{mid}} = -\frac{R_C \parallel R_L}{r_e}$$
* **Atenuación asintótica:**
  * Si las tres frecuencias están separadas: la pendiente comienza en $+20\text{ dB/década}$ para la frecuencia más alta, aumentando a $+40\text{ dB/década}$ y $+60\text{ dB/década}$ por debajo de las frecuencias más bajas.
  * Para $f \ll \min(f_{C1}, f_{C2}, f_{CE})$, la pendiente total es $+60\text{ dB/década}$ ($+18\text{ dB/octava}$).

---

## 5. Respuesta en Alta Frecuencia (Amplificador BJT)

En alta frecuencia, los condensadores externos son cortocircuitos, pero las **capacitancias parásitas internas** del transistor y del cableado comienzan a derivar corriente a tierra.

### 5.1 Capacidades Involucradas y Teorema de Miller
* Capacidades internas del transistor: $C_{be}$ (o $C_\pi$), $C_{bc}$ (o $C_\mu$), y $C_{ce}$.
* Capacidades de cableado: $C_{Wi}$ (entrada) y $C_{Wo}$ (salida).

#### Efecto Miller
La capacitancia de realimentación $C_{bc}$ que une colector y base se descompone en dos condensadores referenciados a tierra:
* **Entrada Miller ($C_{Mi}$):**
  $$C_{Mi} = C_{bc}(1 - A_v) \approx C_{bc}(1 + |A_v|)$$
* **Salida Miller ($C_{Mo}$):**
  $$C_{Mo} = C_{bc}\left(1 - \frac{1}{A_v}\right) \approx C_{bc}$$

### 5.2 Frecuencias de Corte en Alta Frecuencia
1. **Polo de Entrada ($f_{Hi}$):**
   $$R_{Thi} = R_{sig} \parallel R_1 \parallel R_2 \parallel R_i$$
   $$C_i = C_{Wi} + C_{be} + C_{Mi} = C_{Wi} + C_{be} + (1 - A_v)C_{bc}$$
   $$f_{Hi} = \frac{1}{2\pi R_{Thi} C_i}$$

2. **Polo de Salida ($f_{Ho}$):**
   $$R_{Tho} = R_C \parallel R_L \parallel r_o$$
   $$C_o = C_{Wo} + C_{ce} + C_{Mo} = C_{Wo} + C_{ce} + \left(1 - \frac{1}{A_v}\right)C_{bc}$$
   $$f_{Ho} = \frac{1}{2\pi R_{Tho} C_o}$$

3. **Frecuencia de Corte de Beta ($f_\beta$):**
   Límite interno del transporte de portadores en el silicio:
   $$f_\beta = \frac{1}{2\pi \beta_{\text{mid}} r_e (C_\pi + C_\mu)}$$
   *Frecuencia de ganancia unitaria ($f_T$):* $f_T = \beta_{\text{mid}} \cdot f_\beta$.

### 5.3 Frecuencia de Corte Superior Crítica ($f_H$)
La frecuencia de corte superior dominante es la **menor** de las frecuencias de alta:
$$f_H = \min(f_{Hi},\, f_{Ho},\, f_\beta)$$

### 5.4 Diagrama de Bode en Alta Frecuencia
* Para $f < f_H$: la ganancia se mantiene constante en su valor nominal de banda media ($A_{v,\text{mid}}$).
* Para $f > f_H$: la ganancia decae inicialmente a $-20\text{ dB/década}$ (tras el primer polo), incrementando su pendiente negativa a $-40\text{ dB/década}$ y alcanzando hasta $-60\text{ dB/década}$ para frecuencias superiores a los tres polos.