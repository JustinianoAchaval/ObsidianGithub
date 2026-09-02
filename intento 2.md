# Apunte Extendido Clase 4: Diodos, Recta de Carga y Rectificación

> **Nota personal:** Versión detallada de la Clase 4. Incluye las justificaciones matemáticas, el análisis gráfico del punto Q y el comportamiento físico de los portadores en los diodos Zener.

---

## 1. Fundamentos y Modelos del Diodo

La juntura P-N posee una región de empobrecimiento y maneja corrientes típicas desde $\sim 5\text{mA}$ hasta $\sim 200\text{A}$ en polarización directa[cite: 2]. 
*   **Ecuación de Shockley:** Modela matemáticamente el diodo real como $I_D = I_s(e^{\frac{V_D}{nV_T}} - 1)$[cite: 1]. 
*   **Simplificaciones matemáticas:** Si $V_D > 0$, el término $-1$ se desprecia quedando $I_D \approx I_s e^{\frac{V_D}{nV_T}}$[cite: 2]. Si $V_D < 0$, la exponencial tiende a cero resultando en $I_D \approx -I_s$[cite: 2].
*   **Modelos de Ingeniería:** Para no usar Shockley, se asume el modelo de interruptor ideal, o el de interruptor con umbral donde para el Silicio se utiliza $V_u \approx 0.7\text{V}$[cite: 2].

## 2. Análisis de Circuitos y Recta de Carga

Al plantear la Ley de Kirchhoff de Tensiones ($V_s = V_D + I_D R$) junto a la ecuación de Shockley, se forma un sistema de dos ecuaciones no lineales difícil de resolver analíticamente[cite: 1]. 
*   **Trazado de la Recta:** Se establecen dos límites teóricos. El Punto A asume $I_D = 0$, resultando en $V_D = V_s$[cite: 1]. El Punto B asume $V_D = 0$, resultando en $I_D = \frac{V_s}{R}$[cite: 1].
*   **Punto Q (Reposo):** Es la intersección exacta entre la recta trazada y la curva de relación I/V (sea Shockley o los modelos simplificados)[cite: 1].
*   **Aproximaciones:** Si $V_s \gg V_u$, la tensión en la resistencia se aproxima a $V_R \approx V_s$, por ende $I_R \approx \frac{V_s}{R}$[cite: 1].
*   **Asociación de diodos:** Conectarlos en serie divide la tensión total equitativamente y es útil para no superar la Tensión Inversa Pico (PIV típicamente $< 100\text{V}$)[cite: 1]. En paralelo, la corriente total se divide en partes iguales asumiendo tensiones de umbral idénticas[cite: 1].

## 3. Circuitos Rectificadores

Tienen la finalidad de convertir señales de corriente alterna (CA) en corriente continua (CC)[cite: 1].
*   **Media Onda:** Para una señal $v_i(t) = \hat{V}_i \sin(\omega t)$, el diodo está encendido solo entre $0 \le t < T/2$ y apagado entre $T/2 \le t < T$[cite: 1]. Utilizando el modelo ideal, la tensión media generada es $V_m = \frac{\hat{V}_i}{\pi}$[cite: 1].
*   **Onda Completa:** Para aprovechar ambos semiciclos, se utiliza una configuración más avanzada conocida como puente de diodos[cite: 1].

## 4. Regulación con Diodo Zener

Funciona operando en la región de ruptura inversa; al superar la PIV, los portadores minoritarios adquieren tanta energía cinética que colisionan entre sí[cite: 2]. 
*   **Parámetros:** Mantiene una tensión constante de fábrica (ej. $-5\text{V}$, $-1\text{kV}$, $-20\text{kV}$)[cite: 2]. Se define $V_Z = -V_{AK}$ e $I_Z = -I_D$[cite: 1].
*   **Análisis y Regulación:** Para que funcione como regulador de tensión, debe cumplirse $0 \le I_Z \le I_{ZM}$[cite: 1]. Para saber si enciende, se lo retira analíticamente para calcular la tensión a circuito abierto ($V_{ab}$)[cite: 1]. En un análisis límite ($I_Z = I_{ZM}$), la corriente de entrada se calcula como $I_{R1} = I_{ZM} + I_L$[cite: 1].