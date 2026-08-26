# Resumen Clase 3: Diodos y Semiconductores

> **Nota personal:** Este apunte resume los conceptos teóricos, fórmulas principales y modelos prácticos para resolver circuitos con diodos. ¡Ideal para tener a mano al estudiar!

---

## 1. Materiales Semiconductores y Dopado

Para entender el diodo, primero hay que entender el material base (generalmente Silicio o Germanio).
 
* **Electrones de valencia:** Tanto el **Si** como el **Ge** tienen **4 electrones** en su capa de valencia.

![Clase3, p.5](Electronica/Unidad2/Clase3.pdf#page=5&rect=63,32,381,152&color=yellow)

*   **Bandas de Energía:** La energía necesaria para que un electrón salte a la banda de conducción se denomina *Energy Gap* ($E_g$).
    *   Regla de los materiales: $E_{g,a\text{islante}} > E_{g,\text{semiconductor}}$.
    *   Orden de mayor a menor: $E_{g,a}>E_{g,\text{GaAs}} > E_{g,\text{Si}} > E_{g,\text{Ge}}$.

![Clase3, p.7](Electronica/Unidad2/Clase3.pdf#page=7&rect=9,38,447,152&color=yellow)

### Materiales Extrínsecos (Dopados)
*   **Material Tipo N:** Se dopa con impurezas pentavalentes (Sb, As, P) que tienen **5 electrones** de valencia. Son átomos **donadores**.
    *   *Mayoritarios:* Electrones ($-$).
    *   *Minoritarios:* Huecos ($+$).

![Clase3, p.8](Electronica/Unidad2/Clase3.pdf#page=8&rect=60,21,397,141&color=yellow)

*   **Material Tipo P:** Se dopa con impurezas trivalentes (B, Ga, In) de **3 electrones** de valencia. Son átomos **aceptores** porque dejan un hueco.
    *   *Mayoritarios:* Huecos ($+$).
    *   *Minoritarios:* Electrones ($-$).

![Clase3, p.9](Electronica/Unidad2/Clase3.pdf#page=9&rect=64,24,383,127&color=yellow)


---

## 2. La Juntura P-N (Polarización)

Al unir material P y N se forma el diodo, el cual puede encontrarse en 3 estados de polarización:

1.  **Sin polarización ($V_{AK} = 0$):** Se forma una región de agotamiento de cargas.
2.  **Polarización Inversa ($V_{AK} < 0$):** La región de empobrecimiento se ensancha.
    *   Circula una corriente limitadísima llamada $I_s$.
    *   💡 **Dato:** $I_s$ va desde $\sim 10\text{pA}$ a $\sim 10\mu\text{A}$.
3.  **Polarización Directa ($V_{AK} > 0$):** 
    *   Permite circular una corriente de difusión dominada por cargas mayoritarias.
    *   💡 **Dato:** $I_D$ es grande, del orden de $\sim 5\text{mA}$ a $\sim 200\text{A}$.

---

## 3. Fórmulas Matemáticas Importantes

### Ecuación de Shockley (Curva del diodo)
$$ I_D = I_s \left( e^{\frac{V_D}{n V_T}} - 1 \right) $$

*Simplificaciones prácticas para cálculos:*
*   **Si $V_D > 0$:** $I_D \approx I_s e^{\frac{V_D}{n V_T}}$.
*   **Si $V_D < 0$:** $I_D \approx -I_s$.

### Potencia Disipada ($P_D$)
La relación básica es $P_D = V_D \cdot I_D$.
*   Diodo Si rectificador en **directa**: $P_D \approx 0.7 \cdot I_D$.
*   Diodo Si rectificador en **inversa**: $P_D \approx 0$.
*   Diodo **Zener**: $P_Z = V_Z \cdot I_Z$.

---

## 4. Modelos Simplificados para Circuitos

Para simplificar el cálculo, en lugar de usar Shockley se utilizan modelos equivalentes:

1.  **Modelo de Interruptor (Ideal):**
    *   Polarización directa: Funciona como un **interruptor cerrado** (cable ideal).
    *   Polarización inversa: Funciona como un **interruptor abierto**.
2.  **Modelo de Interruptor con Umbral (Más común):**
    *   Polarización directa ($V_{AK} > V_U$): Interruptor cerrado en serie con una fuente igual al umbral ($V_U$).
    *   📌 **Para Diodos de Silicio (Si):** La tensión umbral a usar es **$V_U \approx 0.7\text{V}$**.
    *   Polarización inversa ($V_{AK} < V_U$): Interruptor abierto.

---

## 5. La Recta de Carga y Punto Q

Para un circuito serie con fuente ($V_s$), diodo y resistencia ($R$), usamos la Ley de Kirchhoff (LKT):
$$ V_s = V_D + I_D \cdot R $$

Para dibujar la **recta de carga** se determinan sus dos extremos
*   **Corte (Punto A):** Suponiendo $I_D = 0 \Rightarrow V_D = V_s$.
*   **Saturación (Punto B):** Suponiendo $V_D = 0 \Rightarrow I_D = \frac{V_s}{R}$.

El **Punto Q (Punto de reposo)** se halla encontrando la intersección entre esta recta trazada y la curva de relación I/V del diodo (ideal o Shockley).

---

## 6. Diodos Zener

A diferencia de los normales, trabajan en **polarización inversa**.
*   Están diseñados para soportar el efecto avalancha al superar la PIV (Peak Inverse Voltage), manteniendo la tensión constante y regulando el voltaje.
*   **Tensión Zener:** $V_Z = -V_{AK}$.
*   **Corriente Zener:** $I_Z = -I_D$.
*   **Condición de trabajo seguro:** $0 \le I_Z \le I_{ZM}$.
*   💡 **Tip para ejercicios:** Para comprobar si el regulador Zener de un circuito enciende, desconecta analíticamente el diodo y fíjate si el circuito abierto supera el voltaje de $V_Z$.