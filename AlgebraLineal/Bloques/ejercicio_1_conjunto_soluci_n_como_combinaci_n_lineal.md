# Corrección del Ejercicio 1: Cómo escribir el Conjunto Solución como Combinación Lineal

## 1. Revisión rápida de tu resolución en papel

* **Lo que está excelente:** Llegaste correctamente a $\text{rgo}(A) = 2$ y clasificaste bien el sistema como **Compatible Indeterminado**.
* **Un detalle de cuenta:** En el segundo determinante de $3 \times 3$, el primer producto de la diagonal principal es $1 \cdot 4 \cdot 2 = 8$ (anotaste $6$), aunque como la columna 2 es el doble de la columna 1, el determinante da $0$ igual.
* **Consejo clave para ahorrar tiempo en el final:** Calcular cuatro determinantes de $3 \times 3$ te sirve para saber el rango, **pero no te deja el sistema despejado** para armar las soluciones. Si hacés **Gauss-Jordan** desde el principio (como pedía el ítem *a*), en solo 2 pasos obtenés **a la vez** el rango y el sistema listo para escribir la combinación lineal.

---

## 2. Paso previo: Reducción por Gauss-Jordan hasta la MERF ($R_A$)

Partimos de la matriz de coeficientes $A$ (como el sistema es homogéneo, la columna ampliada son todos ceros y no cambia):

$$
A = \begin{pmatrix} 1 & 2 & -1 & 1 \\ 2 & 4 & -1 & 3 \\ -1 & -2 & 2 & 0 \end{pmatrix}
$$

**Paso 1:** Hacemos ceros debajo del primer pivote ($a_{11} = 1$) usando $R_2 \to R_2 - 2R_1$ y $R_3 \to R_3 + R_1$:

$$
\begin{pmatrix} 1 & 2 & -1 & 1 \\ 0 & 0 & 1 & 1 \\ 0 & 0 & 1 & 1 \end{pmatrix}
$$

**Paso 2:** Usamos el segundo pivote ($1$ en fila 2, columna 3) para hacer ceros arriba y abajo, aplicando $R_1 \to R_1 + R_2$ y $R_3 \to R_3 - R_2$:

$$
R_A = \begin{pmatrix} \mathbf{1} & 2 & 0 & 2 \\ 0 & 0 & \mathbf{1} & 1 \\ 0 & 0 & 0 & 0 \end{pmatrix}
$$

Esta matriz $R_A$ ya está en **forma escalonada reducida por filas (MERF)**.

* **Clasificación por Rouché-Capelli:** Como es un sistema homogéneo, siempre es consistente. Contamos las filas no nulas (o pivotes) de $R_A$: $\text{rgo}(A) = \text{rgo}(A \mid 0) = 2 < 4 = n$. Por lo tanto, es **Consistente Indeterminado** con $n - r = 4 - 2 = 2$ parámetros libres.

---

## 3. Los 5 pasos para escribir el Conjunto Solución como Combinación Lineal

Siguiendo exactamente el esquema del apunte de tu cátedra:

### Paso 1: Identificar incógnitas principales y secundarias
Miramos las columnas de $R_A$:
* **Columnas principales** (donde están los pivotes en negrita): columna 1 y columna 3 $\implies$ **Incógnitas principales:** $x_1$ y $x_3$.
* **Columnas no principales** (sin pivote): columna 2 y columna 4 $\implies$ **Incógnitas secundarias (libres):** $x_2$ y $x_4$.

### Paso 2: Escribir el sistema resolvente $R_A X = \mathbf{0}$ y despejar las principales
Cada fila no nula de $R_A$ es una ecuación:

$$
\begin{cases} x_1 + 2x_2 + 2x_4 = 0 \\ x_3 + x_4 = 0 \end{cases}
$$

Despejamos las **incógnitas principales** ($x_1, x_3$) en función de las **secundarias** ($x_2, x_4$):

$$
\begin{cases} x_1 = -2x_2 - 2x_4 \\ x_3 = -x_4 \end{cases}
$$

### Pasos 3 y 4: Asignar parámetros libres a las incógnitas secundarias
Como $x_2$ y $x_4$ varían libremente en $\mathbb{R}$, les ponemos nombre de parámetros:

$$
x_2 = s, \quad x_4 = t \qquad (s, t \in \mathbb{R})
$$

Reemplazando en las cuatro incógnitas en orden, tenemos:

$$
\begin{cases} x_1 = -2s - 2t \\ x_2 = s \\ x_3 = -t \\ x_4 = t \end{cases}
$$

### Paso 5: Armar la $4$-upla y separar por parámetro (Combinación Lineal)
Escribimos el vector genérico $(x_1, x_2, x_3, x_4)$ reemplazando cada componente:

$$
(x_1, x_2, x_3, x_4) = (-2s - 2t,\; s,\; -t,\; t)
$$

Ahora **separamos en una suma de vectores**: el primer vector se queda solo con los términos que tienen $s$ (y $0$ donde no hay $s$), y el segundo vector solo con los términos que tienen $t$ (y $0$ donde no hay $t$):

$$
(x_1, x_2, x_3, x_4) = (-2s,\; s,\; 0,\; 0) + (-2t,\; 0,\; -t,\; t)
$$

Por último, **sacamos factor común** $s$ del primer vector y $t$ del segundo:

$$
(x_1, x_2, x_3, x_4) = s(-2, 1, 0, 0) + t(-2, 0, -1, 1), \quad s, t \in \mathbb{R}
$$

---

## 4. Respuesta final (como queda prolijo en el examen)

El conjunto solución del sistema es:

$$
S = \left\{ s(-2, 1, 0, 0) + t(-2, 0, -1, 1) \in \mathbb{R}^4 \;\middle/\; s, t \in \mathbb{R} \right\}
$$

*(Nota para el Bloque 2: esto mismo se escribe también como subespacio generado $S = \langle (-2, 1, 0, 0), (-2, 0, -1, 1) \rangle$, ¡y esos dos vectores ya forman automáticamente una **base** del espacio solución!)*

---

## 5. Truco de verificación rápida (30 segundos en el final)

Para estar 100% seguro de que no te equivocaste en ningún signo, reemplazá cada vector generador en las ecuaciones originales:
* Con $(-2, 1, 0, 0)$:
  * Ec. 1: $(-2) + 2(1) - 0 + 0 = 0$ $\checkmark$
  * Ec. 2: $2(-2) + 4(1) - 0 + 0 = 0$ $\checkmark$
  * Ec. 3: $-(-2) - 2(1) + 0 = 0$ $\checkmark$
* Con $(-2, 0, -1, 1)$:
  * Ec. 1: $(-2) + 0 - (-1) + 1 = 0$ $\checkmark$
  * Ec. 2: $2(-2) + 0 - (-1) + 3(1) = 0$ $\checkmark$
  * Ec. 3: $-(-2) - 0 + 2(-1) = 0$ $\checkmark$