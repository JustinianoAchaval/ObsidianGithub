# Resumen Clase 2: Circuitos en CA y Transformadores

> **Nota personal:** Apunte enfocado en las fórmulas de la Clase 2. Lo principal acá es no marearse con los desfasajes entre tensión y corriente, y acordarse de memoria las relaciones del transformador ideal para los problemas.

---

## 1. Comportamiento de las Cargas Ideales en CA

En corriente alterna, las señales de tensión y corriente tienen la misma frecuencia, pero suelen estar desfasadas por un ángulo $\phi$.

*   **Carga Inductiva Ideal (L):** La corriente se **atrasa** respecto a la tensión ($\phi = \frac{\pi}{2}$).
    *   Fasor de corriente: $\vec{I} = \hat{I}e^{-j\frac{\pi}{2}}$
*   **Carga Capacitiva Ideal (C):** La corriente se **adelanta** respecto a la tensión ($\phi = -\frac{\pi}{2}$).
    *   Fasor de corriente: $\vec{I} = \hat{I}e^{j\frac{\pi}{2}}$
*   **Circuito RLC:** El desfasaje total depende de los componentes y se mantiene en el rango $-\frac{\pi}{2} < \phi < \frac{\pi}{2}$.

---

## 2. Circuito RLC Serie e Impedancia Compleja

Para modelar un circuito RLC serie, usamos la Ley de Kirchhoff de Tensiones (LKT), sumando las caídas instantáneas en cada elemento:
$$ v_s(t) = v_R(t) + v_L(t) + v_C(t) $$

Sabiendo que las tensiones instantáneas son:
*   **Resistencia:** $v_R(t) = R \cdot i(t)$
*   **Inductancia:** $v_L(t) = L \cdot \frac{di(t)}{dt}$
*   **Capacitancia:** $v_C(t) = \frac{1}{C} \int i(t)dt$

**Ley de Ohm en CA:** Para no trabajar con ecuaciones diferenciales en el tiempo, pasamos al dominio fasorial. Aquí usamos la **Impedancia Compleja ($Z$)**, que modela la oposición total al paso de la corriente:
$$ Z = R + j\left(\omega L - \frac{1}{\omega C}\right) $$

---

## 3. Transformadores y Acoplamiento

El transformador permite relacionar tensiones y corrientes entre dos mallas de un circuito manteniendo la aislación galvánica (no hay contacto eléctrico directo, solo magnético).

*   **Coeficiente de Acoplamiento ($k$):** Mide la eficacia del flujo magnético confinado entre las bobinas. 
    $$ k = \frac{M}{\sqrt{L_1 L_2}} $$
*   **Impedancia Reflejada ($Z_r$):** Es el efecto de la impedancia de carga del secundario ($Z_L$) "vista" desde la fuente en el primario.
*   **Autotransformador:** Tiene las bobinas acopladas en serie. Comparte acoplamiento tanto magnético como eléctrico, logrando ajustar tensiones con menos espiras, pero perdiendo la aislación galvánica.

### El Transformador Ideal
Se asume que no hay pérdidas ($R_1 = R_2 = 0$), el acoplamiento es perfecto ($k = 1$) y las inductancias son infinitas. 
Las fórmulas clave para relacionar primario ($s$, $1$) y secundario ($L$, $2$) a través del número de espiras ($N$) son:
$$ \frac{\hat{V}_L}{\hat{V}_s} = \frac{N_2}{N_1} $$

$$ \frac{\hat{I}_L}{\hat{I}_s} = \frac{N_1}{N_2} $$