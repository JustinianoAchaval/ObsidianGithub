# Resumen Clase 1: Introducción a la Corriente Alterna

> **Nota personal:** Este apunte resume los conceptos iniciales sobre CA, las representaciones matemáticas de las señales y las definiciones fundamentales (como valor medio y valor eficaz). ¡Ideal como introducción teórica antes de avanzar a los circuitos RLC!

---

## 1. Generación y Características de las Señales Sinusoidales

*   **Generación de Energía:** Típicamente se basa en un conductor eléctrico formando una espira, el cual se encuentra inmerso en un flujo magnético variante.
*   Esta variación de flujo suele deberse a un movimiento rotativo mecánico, el cual es impulsado por algún otro tipo de energía (térmica, eólica, hidráulica, mareomotriz, nuclear, etc.).
*   **Parámetros de la señal:** Una señal sinusoidal se caracteriza por su amplitud (o valor pico), su periodo, su frecuencia y su pulsación angular.
*   **Ángulo en el tiempo:** Si se supone una espira rotando, el ángulo en función del tiempo se define como $\alpha(t) = \omega t$.

---

## 2. Representación de Sinusoides y Desfasajes

Al comparar varias sinusoides de la **misma frecuencia**, estas pueden encontrarse adelantadas o atrasadas entre sí. Se pueden analizar mediante:
*   **Representación Cartesiana:** Trazado de las ondas sobre ejes de coordenadas clásicos.
*   **Representación Vectorial (Fasorial):** Representación geométrica donde los fasores rotan a una velocidad angular $\omega$.

**Matemáticamente, para tensiones de igual frecuencia:**
*   Señal tomada como referencia: $v_1(t) = \hat{V}_1 \cos(\omega t)$.
*   Señal en **adelanto**: $v_2(t) = \hat{V}_2 \cos(\omega t + \alpha)$, asumiendo $\alpha > 0$.
*   Señal con **retraso**: $v_3(t) = \hat{V}_3 \cos(\omega t - \beta)$, asumiendo $\beta > 0$.

---

## 3. Carga Resistiva Ideal

*   💡 **Dato fundamental:** En un circuito que posee una carga puramente resistiva, la tensión y la corriente siempre están en **fase**.
*   **Potencia instantánea:** Se calcula instante a instante como $p(t) = R \cdot i^2(t)$.
*   **Potencia media ($P_M$):** Se obtiene integrando la potencia instantánea a lo largo de un periodo $T$:
    $$ P_M = \frac{1}{T} \int_{0}^{T} R \cdot i^2(t) dt = \frac{R}{T} \int_{0}^{T} i^2(t) dt $$.

---

## 4. Conceptos de Valor Medio y Valor Eficaz

Es muy importante estudiar el comportamiento de los circuitos en CA debido a los sistemas de distribución de energía eléctrica y para el análisis de señales realistas. Para cuantificarlas se utilizan estos valores:

### Valor Medio
*   El valor medio (o tensión media) sirve para caracterizar el **valor de continua** que está presente en una determinada forma de onda.

### Valor Eficaz ($I_{ef}$ y $V_{ef}$)
*   **Definición conceptual:** El valor eficaz permite realizar una comparación directa entre un circuito en Corriente Alterna (CA) y otro en Corriente Continua (CC) que produzca exactamente la **misma disipación** de potencia.
*   **Planteo:** Si se reemplaza la fuente de tensión alterna por una fuente de CC, se espera que exista una corriente constante ($i(t) = I_{ef}$) que disipe idéntica cantidad de calor.
*   **Fórmula matemática (Corriente Eficaz):** Igualando las potencias ($P_M = I_{ef}^2 \cdot R$), se obtiene:
    $$ I_{ef} = \sqrt{ \frac{1}{T} \int_{0}^{T} i^2(t) dt } $$.
*   📌 **Nota:** A partir de esta misma definición y procedimiento, se puede establecer de forma análoga la expresión para la **tensión eficaz ($V_{ef}$)**.