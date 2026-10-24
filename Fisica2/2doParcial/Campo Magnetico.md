# Resumen de Fórmulas - Unidad VI: El Campo Magnético

## Constantes Fundamentales
* **Permeabilidad magnética del vacío:** $\mu_0 = 4\pi \cdot 10^{-7} \text{ T}\cdot\text{m/A}$
* **Constante magnética:** $k' = \frac{\mu_0}{4\pi} = 10^{-7} \text{ T}\cdot\text{m/A}$

---

## 1. Leyes Elementales (Biot-Savart)
* **Campo magnético de una carga puntual $q$ en movimiento:**
  $$\vec{B} = \frac{\mu_0}{4\pi} \frac{q (\vec{v} \times \hat{r})}{r^2} \quad \implies \quad B = 10^{-7} \frac{|q| v \sin(\phi)}{r^2}$$
* **Campo magnético de un elemento de corriente (Ley de Biot-Savart):**
  $$d\vec{B} = \frac{\mu_0}{4\pi} \frac{I (d\vec{l} \times \hat{r})}{r^2} \quad \implies \quad dB = 10^{-7} \frac{I dl \sin(\phi)}{r^2}$$

---

## 2. Aplicaciones Geométricas Clásicas
* **Conductor rectilíneo de longitud finita** (a una distancia radial $a$):
  $$B_P = \frac{\mu_0 I}{4\pi a} (\cos\alpha - \cos\beta) = \frac{k' I}{a} (\cos\alpha - \cos\beta)$$
  *(Donde $\alpha$ y $\beta$ son los ángulos internos/externos desde los extremos del cable hacia el punto $P$).*

* **Conductor rectilíneo infinitamente largo** (a una distancia radial $a$ o $r$):
  $$B = \frac{\mu_0 I}{2\pi a}$$

* **Espira o Bobina circular sobre su eje central** (radio $a$, a una distancia $x$ del centro, con $N$ vueltas):
  $$B_x = \frac{\mu_0 N I a^2}{2(x^2 + a^2)^{3/2}} = \frac{\mu_0 \mu}{2\pi (x^2 + a^2)^{3/2}}$$
  *(Donde el momento dipolar magnético es $\mu = N I A = N I \pi a^2$).*

* **Centro de una espira/bobina circular completa** ($x = 0$, radio $a$):
  $$B = \frac{\mu_0 N I}{2a}$$

* **Arco de circunferencia de ángulo $\theta$ (en radianes) en su centro de curvatura:**
  $$B = \frac{\mu_0 I \theta}{4\pi a}$$
  *(Nota: Para media espira $\theta = \pi \implies B = \frac{\mu_0 I}{4a}$).*

---

## 3. Solenoides y Toroides
* **Solenoide Corto** (en un punto sobre su eje central, longitud $L$, radio $R$, $N$ vueltas):
  * En el punto medio del solenoide corto:
    $$B = \mu_0 \frac{N}{L} I \frac{1}{\sqrt{\frac{4R^2}{L^2} + 1}}$$
* **Solenoide Largo (Ideal, $L \gg R$)** en su interior:
  $$B = \mu_0 n I = \mu_0 \frac{N}{L} I$$
* **Toroide** (en su núcleo interior, a distancia $r$ o $R_{medio}$ del centro):
  $$B = \frac{\mu_0 N I}{2\pi r}$$
  *(Fuera del núcleo del toroide, $B = 0$).*

---

## 4. Ley de Ampère
* **Forma Integral:**
  $$\oint \vec{B} \cdot d\vec{l} = \mu_0 I_{neta\_encerrada}$$
* **Forma Diferencial:**
  $$\nabla \times \vec{B} = \mu_0 \vec{J}$$
* **Conductor cilíndrico macizo de radio $R$** (con corriente $I$ uniforme en su sección):
  * **Interior ($r \le R$):** $B = \frac{\mu_0 I}{2\pi R^2} r$ *(crece linealmente con $r$)*
  * **Exterior ($r \ge R$):** $B = \frac{\mu_0 I}{2\pi r}$ *(decrece con $1/r$)*
* **Cilindro hueco de radio interno $R_1$ y externo $R_2$**:
  * **$r \le R_1$:** $B = 0$
  * **$R_1 < r < R_2$:** $B = \frac{\mu_0}{2\pi r} I_{neta} = \frac{\mu_0 I}{2\pi r} \left(\frac{r^2 - R_1^2}{R_2^2 - R_1^2}\right)$
  * **$r \ge R_2$:** $B = \frac{\mu_0 I}{2\pi r}$