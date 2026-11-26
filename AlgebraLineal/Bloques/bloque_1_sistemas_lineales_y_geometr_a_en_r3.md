# Bloque 1 (Día 1): Sistemas Lineales (Instrumental) y Geometría en $\mathbb{R}^3$

**Tiempo sugerido:** 4 horas (1h Teoría · 2h 30m Práctica · 30m Ficha de Cierre)  
**Objetivo del día:** Ganar velocidad y precisión en la reducción por Gauss-Jordan y el análisis de sistemas homogéneos (herramienta clave para subespacios, $W^\perp$ y núcleos), y dominar las ecuaciones y relaciones geométricas de rectas y planos en $\mathbb{R}^3$ (enfoque **Ítem 4a** del Examen Modelo Regular).

---

## Parte A: Sistemas de Ecuaciones Lineales (Resumen Teórico Instrumental)

### 1. Representación Matricial y Operaciones Elementales
Un sistema de $m$ ecuaciones lineales con $n$ incógnitas se escribe como:
$$AX = H$$
donde $A \in \mathbb{R}^{m \times n}$ es la matriz de coeficientes, $X \in \mathbb{R}^{n \times 1}$ el vector de incógnitas y $H \in \mathbb{R}^{m \times 1}$ el vector de términos independientes. Su matriz aumentada es $[A \mid H]$.

Para obtener sistemas **equivalentes** (que poseen exactamente el mismo conjunto solución), aplicamos las tres **operaciones elementales por filas**:
1. Multiplicar una fila por un escalar no nulo: $R_i \to c R_i \quad (c \neq 0)$.
2. Sumar a una fila un múltiplo escalar de otra: $R_j \to R_j + c R_i$.
3. Permutar dos filas: $R_i \leftrightarrow R_j$.

* **Eliminación Gaussiana:** lleva $[A \mid H]$ a la **forma escalonada por renglones** (ceros debajo de cada pivote).
* **Eliminación de Gauss-Jordan:** lleva $[A \mid H]$ a la **forma escalonada reducida por renglones** (cada pivote es $1$ y es el único elemento no nulo de su columna).

### 2. Teorema de Rouché-Capelli
El rango de una matriz, $\text{rgo}(A)$, es igual al número de filas no nulas de su forma escalonada (cantidad de pivotes).

> **Teorema de Rouché-Capelli:** El sistema $AX = H$ es consistente (tiene al menos una solución) si y sólo si:
> $$\text{rgo}(A) = \text{rgo}(A \mid H)$$

| Clasificación | Condición de Rangos | Soluciones |
| :--- | :--- | :--- |
| **Consistente Determinado** | $\text{rgo}(A) = \text{rgo}(A \mid H) = n$ | Solución única. |
| **Consistente Indeterminado** | $\text{rgo}(A) = \text{rgo}(A \mid H) = r < n$ | Infinitas soluciones con $n - r$ variables libres (parámetros). |
| **Inconsistente** | $\text{rgo}(A) \neq \text{rgo}(A \mid H)$ | Sin solución ($S = \emptyset$). |

### 3. Sistemas Homogéneos ($AX = \mathbf{0}$)
Un sistema homogéneo **siempre es consistente**, pues al menos admite la **solución trivial** $X = \mathbf{0}$.
* Tiene **solución única (la trivial)** si y sólo si $\text{rgo}(A) = n$.
* Tiene **infinitas soluciones (no triviales)** si y sólo si $\text{rgo}(A) < n$.
* **Corolario clave:** Si $m < n$ (menos ecuaciones que incógnitas), el sistema homogéneo tiene obligatoriamente infinitas soluciones.

> **¿Por qué esto es vital para tu examen regular?**  
> Cada vez que busques el núcleo $\text{nu}(F)$, el complemento ortogonal $W^\perp$, una base de $U \cap W$ o verifiques independencia lineal, vas a estar resolviendo un sistema homogéneo $AX = \mathbf{0}$. El número de variables libres ($n - r$) será directamente la **dimensión** de ese subespacio.

---

## Parte B: Geometría en $\mathbb{R}^3$ — Rectas y Planos

### 1. Ecuaciones de la Recta en $\mathbb{R}^3$
Una recta $r$ queda determinada por un **punto de paso** $P_0(x_0, y_0, z_0)$ y un **vector director** no nulo $\mathbf{v} = (a, b, c)$:

* **Ecuación vectorial:** $(x, y, z) = (x_0, y_0, z_0) + t(a, b, c), \quad t \in \mathbb{R}$.
* **Ecuaciones paramétricas:**
  $$\begin{cases} x = x_0 + at \\ y = y_0 + bt \\ z = z_0 + ct \end{cases} \quad (t \in \mathbb{R})$$
* **Ecuaciones simétricas** (si $a, b, c \neq 0$):
  $$\frac{x - x_0}{a} = \frac{y - y_0}{b} = \frac{z - z_0}{c}$$

> **Atención en exámenes:** Para leer correctamente el vector director $\mathbf{v} = (a, b, c)$ en la forma simétrica, los coeficientes que multiplican a $x, y, z$ en los numeradores deben ser exactamente $+1$. Si aparece, por ejemplo, $\frac{2x - 1}{4}$, hay que reescribirlo como $\frac{x - 1/2}{2}$.

### 2. Ecuación del Plano en $\mathbb{R}^3$
Un plano $\pi$ queda determinado por un punto $P_0(x_0, y_0, z_0)$ y un **vector normal** (perpendicular al plano) no nulo $\mathbf{n} = (A, B, C)$:

* **Ecuación implícita o general:**
  $$Ax + By + Cz = D$$
  donde $D = A x_0 + B y_0 + C z_0$.

### 3. Posiciones Relativas (Paralelismo y Perpendicularidad)
Sean las rectas $r_1$ (director $\mathbf{v}_1$), $r_2$ (director $\mathbf{v}_2$) y los planos $\pi_1$ (normal $\mathbf{n}_1$), $\pi_2$ (normal $\mathbf{n}_2$):

| Relación | Condición Vectorial | Justificación Geométrica |
| :--- | :--- | :--- |
| **Recta $\parallel$ Recta** ($r_1 \parallel r_2$) | $\mathbf{v}_1 = k \mathbf{v}_2 \quad (k \neq 0)$ | Los vectores directores son paralelos (múltiplos escalares). |
| **Recta $\perp$ Recta** ($r_1 \perp r_2$) | $\mathbf{v}_1 \cdot \mathbf{v}_2 = 0$ | Los vectores directores son ortogonales. |
| **Plano $\parallel$ Plano** ($\pi_1 \parallel \pi_2$) | $\mathbf{n}_1 = k \mathbf{n}_2 \quad (k \neq 0)$ | Los vectores normales son paralelos (mismo subespacio director). |
| **Plano $\perp$ Plano** ($\pi_1 \perp \pi_2$) | $\mathbf{n}_1 \cdot \mathbf{n}_2 = 0$ | Los vectores normales son ortogonales. |
| **Recta $\perp$ Plano** ($r \perp \pi$) | $\mathbf{v} = k \mathbf{n} \quad (k \neq 0)$ | El director de la recta debe ser **paralelo** a la normal del plano. |
| **Recta $\parallel$ Plano** ($r \parallel \pi$) | $\mathbf{v} \cdot \mathbf{n} = 0$ | El director de la recta debe ser **ortogonal** a la normal del plano. |

*(¡Ojo con las últimas dos filas! Es el error más común en parciales y finales: para que una recta sea **perpendicular** a un plano, su vector director debe ser **paralelo** a la normal del plano, no perpendicular.)*

---

## Práctica Guiada del Bloque 1 (Estilo Examen Final Regular)

Intentá resolver estos 4 ejercicios en papel, **justificando cada paso como si estuvieras rindiendo el final**. Cuando termines (o si te trabás en alguno), mandame tus respuestas y te las corrijo con el criterio de la cátedra.

### Ejercicio 1 (Sistema Homogéneo — Entrenamiento Instrumental)
Dado el siguiente sistema homogéneo en $\mathbb{R}^4$:
$$\begin{cases} x_1 + 2x_2 - x_3 + x_4 = 0 \\ 2x_1 + 4x_2 - x_3 + 3x_4 = 0 \\ -x_1 - 2x_2 + 2x_3 = 0 \end{cases}$$
a) Llevar la matriz de coeficientes a la **forma escalonada reducida por renglones** (Gauss-Jordan).  
b) Indicar $\text{rgo}(A)$, clasificar el sistema mediante el Teorema de Rouché-Capelli y escribir el conjunto solución expresado como combinación lineal de vectores de $\mathbb{R}^4$.

### Ejercicio 2 (Análisis con Parámetro — Rouché-Capelli)
Determinar los valores del parámetro $k \in \mathbb{R}$ para los cuales el siguiente sistema es: (i) consistente determinado, (ii) consistente indeterminado y (iii) inconsistente. Justificar citando el Teorema de Rouché-Capelli.
$$\begin{cases} x + y + z = 2 \\ 2x + 3y + 2z = 5 \\ 2x + 3y + (k^2 - 2)z = k + 3 \end{cases}$$

### Ejercicio 3 (Verdadero / Falso — Estilo Ítem 4a del Examen Modelo)
Analizar la verdad o falsedad de las siguientes afirmaciones. **Justificar claramente:**
a) *(Idéntico al Examen Modelo)* La recta $r: x + 2 = \frac{y - 1}{2} = \frac{z}{3}$ pasa por el punto $Q = (-1, 3, 3)$ y es perpendicular al plano $\pi: 2x + 4y + 6z = 5$.  
b) La recta $r_2: \begin{cases} x = 1 + 2t \\ y = -3t \\ z = 4 - t \end{cases}$ ($t \in \mathbb{R}$) es paralela al plano $\pi_2: 2x + y + z = 7$ y está contenida en él.

### Ejercicio 4 (Conceptual de Variedades Lineales)
Dados dos planos en $\mathbb{R}^3$:
$$\pi_1: x - 2y + 3z = 4 \quad \text{y} \quad \pi_2: -2x + 4y - 6z = 1$$
a) Explicar por qué $\pi_1$ y $\pi_2$ son variedades lineales paralelas usando la relación entre sus subespacios directores ($W_{\pi_1}$ y $W_{\pi_2}$).  
b) ¿Tienen algún punto en común? Justificar tanto geométricamente como usando Rouché-Capelli.

---

## Cierre del Día 1 (Últimos 30 minutos)
Al terminar la práctica, revisá tu propia hoja de respuestas y verificá estos 4 puntos antes de pasar al Bloque 2:
- [ ] ¿Escribiste explícitamente las operaciones elementales usadas en cada paso ($R_2 \to R_2 - 2R_1$, etc.)?
- [ ] ¿Citaste el Teorema de Rouché-Capelli comparando $\text{rgo}(A)$, $\text{rgo}(A \mid H)$ y $n$?
- [ ] ¿Verificaste las **dos condiciones** en las afirmaciones compuestas con un "y" (por ejemplo, en el 3a: que el punto pertenezca **y** que sea perpendicular)?
- [ ] ¿Tenés clara la diferencia entre condición de paralelismo y perpendicularidad cuando se cruzan **recta** y **plano**?