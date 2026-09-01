# Fórmulas de Tensión, Corriente, Potencia y Resistencia en CA

> **Nota personal:** Recopilación de las fórmulas fundamentales para circuitos en Corriente Alterna, incluyendo los conceptos de valores medios y eficaces.

---

## 1. Relaciones Básicas (Ley de Ohm y Potencia)

*   **Tensión (Ley de Ohm en el tiempo):** $v(t) = R \cdot i(t)$
*   **Corriente (Ley de Ohm en el tiempo):** $i(t) = \frac{v(t)}{R}$
*   **Potencia Instantánea:** $p(t) = v(t) \cdot i(t) = R \cdot i^2(t)$

---

## 2. Fórmulas de Valor Medio

El valor medio representa la componente de corriente continua (CC) de la señal.

*   **Tensión Media ($V_M$):**
    $$ V_M = \frac{1}{T} \int_{0}^{T} v(t) dt $$
*   **Corriente Media ($I_M$):**
    $$ I_M = \frac{1}{T} \int_{0}^{T} i(t) dt $$
*   **Potencia Media ($P_M$):**
    $$ P_M = \frac{1}{T} \int_{0}^{T} p(t) dt = \frac{1}{T} \int_{0}^{T} R \cdot i^2(t) dt = \frac{R}{T} \int_{0}^{T} i^2(t) dt $$

---

## 3. Fórmulas de Valor Eficaz (RMS)

El valor eficaz es el valor de CA que produce la misma disipación de potencia (calor) en una resistencia que una fuente equivalente de CC.

*   **Corriente Eficaz ($I_{ef}$):**
    $$ I_{ef} = \sqrt{ \frac{1}{T} \int_{0}^{T} i^2(t) dt } $$
*   **Tensión Eficaz ($V_{ef}$):**
    $$ V_{ef} = \sqrt{ \frac{1}{T} \int_{0}^{T} v^2(t) dt } $$
*   **Relación de Potencia Media con Valores Eficaces:**
    $$ P_M = V_{ef} \cdot I_{ef} = I_{ef}^2 \cdot R =\frac{V_{ef}}{R}  $$

---

## 4. Impedancia y Ley de Ohm en Fasores (Dominio Frecuencial)

Para evitar trabajar con ecuaciones diferenciales en el tiempo, se utiliza la representación de impedancia compleja ($Z$) y fasores ($\vec{V}$, $\vec{I}$).

*   **Impedancia Compleja ($Z$):**
    $$ Z = \frac{\vec{V}}{\vec{I}} $$
    *(Donde $Z$ se mide en Ohmios [$\Omega$] y tiene una parte real resistiva y una imaginaria reactiva).*
*   **Tensión Fasorial:**
    $$ \vec{V} = \vec{I} \cdot Z $$
*   **Corriente Fasorial:**
    $$ \vec{I} = \frac{\vec{V}}{Z} $$