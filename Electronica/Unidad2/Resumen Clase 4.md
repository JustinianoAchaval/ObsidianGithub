# Resumen Clase 4: Circuitos Rectificadores y Regulación con Zener

> **Nota personal:** Apunte de la Clase 4, enfocado en configuraciones prácticas con diodos: conexión en paralelo, rectificadores de onda completa y el análisis del diodo Zener como regulador de tensión. 

---

## 1. Diodos en Paralelo

Esta configuración es muy útil para dividir y reducir la corriente individual que atraviesa cada diodo, recordando que existe un límite físico de corriente que soportan (típicamente $I_D < 200\text{A}$).

*   Se asume una señal de entrada $v_i(t) = \hat{V}_i \sin(\omega t)$.
*   El diodo conduce únicamente en el semiciclo positivo ($0 \le t < T/2$).
*   **Tensión media (Valor de CC observado en la carga):**
    $$ V_m \approx \frac{\hat{V}_i - V_u}{\pi} $$

---

## 2. Rectificadores de Onda Completa

Existen dos configuraciones principales para aprovechar ambos semiciclos de la onda de alterna de entrada, logrando una señal de salida que siempre es positiva.

### A. Con Transformador de Derivación Central (Punto Medio)
*   Utiliza un transformador que provee dos sinusoides desfasadas 180° respecto a un punto central.
*   Alterna la conducción entre dos diodos ($D_1$ y $D_2$) dependiendo de qué semiciclo esté activo.
*   **Tensión media en la carga:** 
    $$ V_m = \frac{2\hat{V}_i}{\pi} $$
*   **Tensión Inversa Pico (PIV):** El diodo que se encuentra en estado de no conducción debe soportar el doble de la tensión pico: $PIV = 2\hat{V}_i$.

### B. Configuración Puente (Puente de Diodos)
*   Utiliza 4 diodos ($D_1, D_2, D_3, D_4$).
*   **Terminales de CC:** Son los nodos donde se unen ánodos con ánodos o cátodos con cátodos.
*   **Terminales de CA:** Son los nodos donde se unen ánodos con cátodos.
*   **Ciclo de conducción (Dispositivos ideales):**
    *   Semiciclo positivo ($0 \le t < T/2$): Conducen cruzados $D_1$ y $D_2$.
    *   Semiciclo negativo ($T/2 \le t < T$): Conducen cruzados $D_3$ y $D_4$.
*   **Tensión media en la carga:** 
    $$ V_m = \frac{2\hat{V}_i}{\pi} $$
*   **Tensión Inversa Pico (PIV):** A diferencia del punto medio, aquí la exigencia de aislación para los diodos apagados es menor: $PIV = \hat{V}_i$.

---

## 3. El Diodo Zener como Regulador de Tensión

El uso más común del diodo Zener es como regulador, dedicado a proveer una tensión constante en una carga independientemente de las variaciones de la fuente o de la corriente que atraviese el dispositivo.

### Modelo Simplificado y Parámetros
*   **Tensión Zener:** $V_Z = -V_{AK}$
*   **Corriente Zener:** $I_Z = -I_D$
*   **Corriente Zener máxima:** $I_{ZM} = I_{Z,\text{max}}$

### Condición de Regulación
Para garantizar que el Zener funcione correctamente y no sufra daños por sobrecalentamiento, su corriente de trabajo siempre debe mantenerse dentro del rango seguro:
$$ 0 \le I_Z \le I_{ZM} $$

### Método de Análisis en Circuitos
Para circuitos básicos compuestos por una fuente ($v_i$), una resistencia en serie ($R_1$) y una carga en paralelo al Zener ($R_L$):
1.  **Comprobación de encendido:** Para determinar si el Zener "enciende" (es decir, si entra en zona de regulación), se retira analíticamente el Zener del circuito.
2.  Se calcula la tensión a circuito abierto ($V_{ab}$) en los terminales donde estaba conectado.
3.  Si esa tensión $V_{ab}$ es mayor o igual a $V_Z$, significa que el Zener enciende. 
4.  Si enciende, se lo reemplaza por su modelo equivalente (una fuente de tensión ideal de valor $V_Z$) para terminar de calcular las corrientes del circuito.