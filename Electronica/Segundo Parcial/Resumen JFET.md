# Guía Completa de Transistores JFET: Teoría, Circuitos y Polarización en DC

Este documento consolida los fundamentos teóricos, ecuaciones de gobierno y métodos sistemáticos de análisis de circuitos en corriente continua (DC) para transistores **JFET** (_Junction Field Effect Transistor_), incluyendo el método analítico y gráfico para polarización fija, autopolarización y divisor de tensión.

## 1. Fundamentos y Principio de Operación

El JFET es un dispositivo semiconductor de tres terminales (**Drenador - D**, **Fuente - S**, **Puerta - G**) controlado por voltaje a través de una juntura $P-N$ polarizada en inverso.

### Parámetros Característicos de Fabricación

- $I_{DSS}$ (_Drain-to-Source Saturation Current_): Corriente máxima de saturación entre drenador y fuente cuando la tensión puerta-fuente es nula ($V_{GS} = 0\text{ V}$).
    
- $V_P$ o $V_{GS(off)}$ (_Pinch-off Voltage_): Voltaje puerta-fuente que produce el estrangulamiento total del canal ($I_D \approx 0\text{ A}$). Para canal N es negativo ($V_P < 0$); para canal P es positivo ($V_P > 0$).
    
- **Condición de entrada fundamental:** La unión compuerta-canal siempre opera polarizada en inversa:  
    
    $$I_G \approx 0\text{ A}$$
    
    Esto produce una impedancia de entrada extremadamente alta ($R_{in} \ge 10^8\ \Omega$).
    

## 2. Ecuaciones Rectoras del Dispositivo

### 2.1 Ecuación de Transferencia (Ecuación de Shockley)

En la región de **saturación** o **activa** ($V_{DS} \ge V_{GS} - V_P$), la corriente de drenador se modela de forma no lineal (cuadrática):

$$I_D = I_{DSS} \left(1 - \frac{V_{GS}}{V_P}\right)^2$$

- Si $V_{GS} = 0\text{ V} \implies I_D = I_{DSS}$  
    
- Si $V_{GS} = V_P \implies I_D = 0\text{ A}$  
    
- Si $V_{GS} = 0.3 \cdot V_P \implies I_D \approx \frac{I_{DSS}}{2}$  
    
- Si $V_{GS} = 0.5 \cdot V_P \implies I_D = \frac{I_{DSS}}{4}$  
    

### 2.2 Relación de Corrientes

Puesto que la corriente de puerta es nula ($I_G = 0$):  

$$I_S = I_D$$

## 3. Métodos de Polarización en Continua (DC)

Para determinar el punto de operación $Q(V_{GSQ}, I_{DQ}, V_{DSQ})$, se debe resolver el sistema conformado por:

1. **La ecuación del dispositivo (Shockley).**
    
2. **La ecuación de la malla de entrada (recta de carga de entrada).**
    

### Método 1: Autopolarización (_Self-Bias_)

En esta configuración, no se necesita una fuente externa en la compuerta. La caída de tensión producida por la propia corriente $I_D$ en una resistencia de fuente $R_S$ polariza negativamente la unión.

```
       +V_DD
         |
        [R_D]
         |
         +---- D
              | | |
   G ---+-----| | |  (JFET Canal N)
        |     | | |
       [R_G]     +---- S
        |              |
       GND            [R_S]
                       |
                      GND
```

#### Ecuaciones de Malla:

1. **Malla de Entrada:** Como $I_G = 0$, la caída en $R_G$ es nula ($V_G = 0\text{ V}$).  
    
    $$V_S = I_S \cdot R_S = I_D \cdot R_S$$$$V_{GS} = V_G - V_S = 0 - I_D R_S = -I_D R_S$$
2. **Punto** $Q$ **(Solución Analítica):** Sustituyendo $V_{GS} = -I_D R_S$ en Shockley:  
    
    $$I_D = I_{DSS} \left(1 - \frac{-I_D R_S}{V_P}\right)^2 = I_{DSS} \left(1 + \frac{I_D R_S}{V_P}\right)^2$$
    
    Se obtiene una ecuación cuadrática en $I_D$. La raíz físicamente válida debe cumplir: $V_P \le V_{GS} \le 0$.
    
3. **Malla de Salida:**  
    
    $$V_{DD} - I_D R_D - V_{DS} - I_D R_S = 0$$$$V_{DS} = V_{DD} - I_D(R_D + R_S)$$

### Método 2: Polarización por Divisor de Tensión (_Voltage Divider Bias_)

Es la topología más estable frente a tolerancias de fabricación de $I_{DSS}$ y $V_P$.

```
            +V_DD
           /     \
         [R_1]   [R_D]
           |       |
           +---+---+- D
           |   |  | |
           |   G -| | (JFET Canal N)
         [R_2]    | |
           |       +- S
          GND         |
                     [R_S]
                      |
                     GND
```

#### Paso a Paso para la Resolución:

#### 1. Cálculo de la Tensión de Puerta ($V_G$)

Dado que $I_G = 0\text{ A}$, las resistencias $R_1$ y $R_2$ forman un divisor de tensión ideal no cargado:  

$$V_G = V_{DD} \cdot \left(\frac{R_2}{R_1 + R_2}\right)$$

#### 2. Ecuación de la Malla de Entrada

La tensión en la fuente es:  

$$V_S = I_D \cdot R_S$$

Por lo tanto:  

$$V_{GS} = V_G - V_S = V_G - I_D R_S$$

Despejando $I_D$ para la recta de polarización:  

$$I_D = \frac{V_G - V_{GS}}{R_S}$$

#### 3. Determinación del Punto de Operación $Q$  

- **Enfoque Analítico:** Igualando la recta de entrada con la ecuación de Shockley:  
    
    $$I_{DSS} \left(1 - \frac{V_{GS}}{V_P}\right)^2 = \frac{V_G - V_{GS}}{R_S}$$
    
    Reordenando en la forma general $a \cdot V_{GS}^2 + b \cdot V_{GS} + c = 0$:  
    
    $$a = \frac{I_{DSS}}{V_P^2}$$$$b = -\frac{2 I_{DSS}}{V_P} + \frac{1}{R_S}$$$$c = I_{DSS} - \frac{V_G}{R_S}$$
    
    Se resuelve mediante la fórmula cuadrática:  
    
    $$V_{GS} = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$$
    
    _Criterio de selección:_ Se descarta la raíz exterior al intervalo $[V_P, 0]$. Con $V_{GSQ}$ calculado:  
    
    $$I_{DQ} = \frac{V_G - V_{GSQ}}{R_S}$$
- **Enfoque Gráfico:**
    
    1. Graficar la curva de transferencia de Shockley tabulando 4 puntos característicos:
        
        - $(V_{GS} = 0, I_D = I_{DSS})$  
            
        - $(V_{GS} = 0.3 V_P, I_D \approx 0.5 I_{DSS})$  
            
        - $(V_{GS} = 0.5 V_P, I_D = 0.25 I_{DSS})$  
            
        - $(V_{GS} = V_P, I_D = 0)$  
            
    2. Trazar la recta de carga con dos puntos:
        
        - Si $I_D = 0 \implies V_{GS} = V_G$  
            
        - Si $V_{GS} = 0 \implies I_D = \frac{V_G}{R_S}$  
            
    3. La intersección define de manera directa $(V_{GSQ}, I_{DQ})$.
        

#### 4. Cálculo de Tensiones de Salida

- Tensión Drenador-Fuente:  
    
    $$V_{DS} = V_{DD} - I_D (R_D + R_S)$$
- Tensión de Drenador a tierra:  
    
    $$V_D = V_{DD} - I_D R_D \quad \text{o bien} \quad V_D = V_{DS} + V_S$$
- Tensión de Fuente a tierra:  
    
    $$V_S = I_D R_S$$

#### 5. Verificación de la Región Activa

Para garantizar que el transistor opera como fuente de corriente/amplificador y no en zona óhmica:  

$$V_{DS} \ge V_{GS} - V_P$$

Si no se cumple esta desigualdad, el canal no está estrangulado y el dispositivo opera en la zona lineal (óhmica).

## 4. Ejemplo Práctico de Diseño / Análisis Numérico

### Datos del Circuito:

- $V_{DD} = 16\text{ V}$  
    
- $R_1 = 2.1\text{ M}\Omega$, $R_2 = 270\text{ k}\Omega$  
    
- $R_D = 2.4\text{ k}\Omega$, $R_S = 1.5\text{ k}\Omega$  
    
- Parámetros JFET: $I_{DSS} = 8\text{ mA}$, $V_P = -4\text{ V}$  
    

### Resolución:

1. **Calcular** $V_G$**:**  
    
    $$V_G = 16\text{ V} \cdot \left(\frac{270\text{ k}\Omega}{2100\text{ k}\Omega + 270\text{ k}\Omega}\right) \approx 1.82\text{ V}$$
2. **Recta de entrada:**  
    
    $$V_{GS} = 1.82 - I_D \cdot (1.5\text{ k}\Omega)$$
3. **Intersección con Shockley:**  
    
    $$I_D = 8\text{ mA} \left(1 - \frac{V_{GS}}{-4}\right)^2$$
    
    Resolviendo el sistema se obtiene:
    
    - $V_{GSQ} \approx -1.8\text{ V}$  
        
    - $I_{DQ} = \frac{1.82\text{ V} - (-1.8\text{ V})}{1.5\text{ k}\Omega} \approx 2.41\text{ mA}$  
        
4. **Tensiones en los terminales:**
    
    - $V_S = (2.41\text{ mA})(1.5\text{ k}\Omega) \approx 3.62\text{ V}$  
        
    - $V_D = 16\text{ V} - (2.41\text{ mA})(2.4\text{ k}\Omega) \approx 10.22\text{ V}$  
        
    - $V_{DS} = V_D - V_S = 10.22\text{ V} - 3.62\text{ V} = 6.60\text{ V}$  
        
5. **Verificación de estrangulamiento:**  
    
    $$V_{DS} \ge V_{GS} - V_P \implies 6.60\text{ V} \ge -1.8\text{ V} - (-4\text{ V}) = 2.2\text{ V} \quad \text{(Verificado: Zona de Saturación)}$$

## 5. Resumen de Fórmulas para Resolución Rápida

|                        |                                                               |                                     |
| ---------------------- | ------------------------------------------------------------- | ----------------------------------- |
| **Configuración**      | **Ecuación de Malla Entrada (VGS​)**                          | **Ecuación de Malla Salida (VDS​)** |
| **Fija** ($V_{GG}$)    | $V_{GS} = -V_{GG}$                                            | $V_{DS} = V_{DD} - I_D R_D$         |
| **Autopolarización**   | $V_{GS} = -I_D R_S$                                           | $V_{DS} = V_{DD} - I_D (R_D + R_S)$ |
| **Divisor de Tensión** | $V_{GS} = V_{DD}\left(\frac{R_2}{R_1 + R_2}\right) - I_D R_S$ | $V_{DS} = V_{DD} - I_D (R_D + R_S)$ |