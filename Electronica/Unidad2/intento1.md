# Resumen Clase 4: Diodos, Recta de Carga y Rectificación

> **Nota personal:** Apunte definitivo de la Clase 4. Abarca desde el análisis gráfico con recta de carga y configuraciones de múltiples diodos, hasta rectificación de alterna y regulación con Zener.

---

## 1. Análisis del Diodo y Recta de Carga

Para resolver analíticamente un circuito serie (fuente $V_s$, resistencia $R$ y diodo), la Ley de Kirchhoff ($V_s = V_D + I_D R$) combinada con la ecuación de Shockley genera un sistema complejo de ecuaciones no lineales[cite: 1]. La alternativa práctica es el método gráfico:

*   **Trazado de la Recta de Carga:** Se logra evaluando los dos extremos teóricos del circuito[cite: 1].
    *   Punto A (Corte con eje X): Si se supone $I_D = 0$, la tensión en el diodo es $V_D = V_s$[cite: 1].
    *   Punto B (Corte con eje Y): Si se supone $V_D = 0$, la corriente es $I_D = \frac{V_s}{R}$[cite: 1].
*   **Punto de Reposo (Q):** Es la intersección exacta entre la recta trazada y la curva característica de relación I/V del diodo[cite: 1].
*   **Cálculos de Ingeniería:** Para simplificar el cálculo sin graficar, se asume el modelo con umbral ($V_u \approx 0.7\text{V}$ para Silicio)[cite: 2]. En polarización directa, la corriente del circuito se aproxima fácilmente como $I_R = \frac{V_s - V_u}{R}$[cite: 1].

---

## 2. Configuraciones con Múltiples Diodos

*   **Diodos en Serie:** Es una estrategia muy útil para reducir la exigencia de Tensión Inversa Pico (PIV) que debe soportar cada diodo (típicamente estas tensiones soportadas son menores a 100V)[cite: 1]. Al requerir diodos con características similares, la tensión se reparte en partes iguales entre ellos[cite: 1].
*   **Diodos en Paralelo:** Se utiliza para reducir la corriente que atraviesa cada dispositivo individual, recordando que existe un límite físico máximo (aproximadamente 200A)[cite: 1]. Requieren tensiones de umbral similares para asegurar que la corriente total se divida equitativamente[cite: 1].

---

## 3. Circuitos Rectificadores

Tienen como objetivo principal funcionar como conversores de señales de corriente alterna (CA) a corriente continua (CC)[cite: 2].

*   **Media Onda:** El diodo permite la conducción únicamente durante el semiciclo positivo[cite: 1].
*   **Onda Completa (Punto Medio):** Utiliza un transformador de derivación central para alternar la conducción entre dos diodos, generando una tensión media en la carga de $V_m = \frac{2\hat{V}_i}{\pi}$[cite: 1]. El diodo inactivo debe soportar una PIV exigente de $2\hat{V}_i$[cite: 1].
*   **Onda Completa (Puente):** Usa 4 diodos trabajando en pares cruzados por semiciclo[cite: 1]. Logra la misma tensión media de salida, pero reduce drásticamente la exigencia de aislación para los diodos apagados a $PIV = \hat{V}_i$[cite: 1].

---

## 4. El Diodo Zener

A diferencia de los rectificadores, el Zener está dedicado a proveer una tensión constante en un circuito, manteniéndose independiente de la corriente que lo atraviesa[cite: 2]. 
*   **Región de trabajo:** Funciona polarizado en inversa[cite: 2]. Al superar la PIV, los portadores minoritarios ganan tanta velocidad y energía cinética que colisionan entre sí[cite: 2].
*   **Regulación:** Puede mantener de forma constante distintos niveles de voltaje prefijados de fábrica (desde -5V hasta -20kV)[cite: 2]. Su condición de uso seguro dictamina que no debe superar su corriente límite ($0 \le I_Z \le I_{ZM}$)[cite: 1].