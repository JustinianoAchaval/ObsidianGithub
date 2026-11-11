# 📊 Guía de Consulta Rápida: Los 6 Bloques de Cálculo Numérico

Esta guía responde directamente a las **4 preguntas de opción múltiple (desplegables)** de los ejercicios teóricos del parcial.

---

## 1. Tabla Maestra para Responder los 4 Desplegables del Examen

| ¿A qué tipo de problema de cálculo numérico corresponde? | Elija el método o los métodos que sean aplicables a la resolución de este problema | ¿Tipo de error que predomina en el/los método/s de resolución para este problema? | En base al error que predomina, ¿Qué sugiere realizar para minimizar el error en este problema particular? |
| :--- | :--- | :--- | :--- |
| **1. Raíces de ecuaciones** *(No lineales: hallar $x$ tal que $f(x) = 0$)* | • **Cerrados:** Bisección, Falsa Posición (*Regula Falsi*).<br>• **Abiertos:** Punto Fijo, Newton-Raphson, Método de la Secante. | **Error de Truncamiento** *(por detener las iteraciones antes de infinitos pasos y por aproximar con rectas/serie de Taylor)*.<br>*(Nota: En Secante muy cerca de la raíz también puede aparecer redondeo por cancelación por resta).* | • **Disminuir la tolerancia / criterio de error aceptable ($e_s$)**.<br>• **Aumentar el número de iteraciones**.<br>• Emplear un método de convergencia más rápida (ej. Newton-Raphson) o elegir un mejor valor/intervalo inicial más cercano a la raíz. |
| **2. Sistemas de ecuaciones algebraicas lineales** *($A \cdot x = b$)* | • **Métodos Directos (Exactos):** Eliminación de Gauss simple, Gauss-Jordan, Descomposición $LU$.<br>• **Métodos Iterativos:** Gauss-Seidel (o Jacobi). | • **En Métodos Directos (Gauss / $LU$):** Predomina el **Error de Redondeo** *(NO tienen error de truncamiento porque dan la solución en un número finito de pasos)*.<br>• **En Métodos Iterativos (Gauss-Seidel):** Predomina el **Error de Truncamiento** *(por cortar el ciclo iterativo)*. | • **Para Gauss / $LU$ (Redondeo):** Utilizar **variables de doble precisión (`double`)**, aplicar **Pivoteo Parcial (o Escalamiento)** para evitar pivotes pequeños/ceros y reducir el efecto del mal condicionamiento.<br>• **Para Gauss-Seidel (Truncamiento):** Disminuir la tolerancia ($e_s$) y aumentar el número de iteraciones. |
| **3. Ajuste de curvas: Interpolación polinomial** *(Datos exactos tabulados: hallar un valor intermedio entre puntos)* | • **Polinomio interpolante de Newton** (en diferencias divididas).<br>• **Polinomio interpolante de Lagrange**.<br>• **Trazadores (Splines) cúbicos** (por tramos). | **Error de Truncamiento** *(por aproximar una función cualquiera mediante un polinomio de grado finito $n$, cuyo residuo es proporcional a la derivada $(n+1)$)*. | • **Agregar más puntos de soporte (aumentar el grado del polinomio)** si la función es suave.<br>• **Elegir puntos de la tabla más cercanos** al valor de consulta $x$ (reducir el espaciamiento $h$).<br>• Si hay muchos puntos o cambios bruscos, usar **Splines cúbicos** para evitar oscilaciones (fenómeno de Runge). |
| **4. Ajuste de curvas: Regresión** *(Datos experimentales con ruido o dispersión)* | • **Regresión por Mínimos Cuadrados** (Regresión lineal simple, polinomial o linealizada). | **Error de los datos (ruido experimental)** y **Error de Truncamiento / Modelado** *(si el modelo matemático elegido no representa la tendencia real)*. | • **Aumentar la cantidad de mediciones** o mejorar la precisión de los instrumentos.<br>• **Cambiar el grado o tipo de función del modelo** (ej. pasar de regresión lineal a cuadrática o exponencial) verificando el coeficiente de correlación $r^2$. |
| **5. Diferenciación numérica** *(Estimar la tasa de cambio o derivada $f'(x)$)* | • **Diferencias finitas hacia adelante** ($O(h)$).<br>• **Diferencias finitas hacia atrás** ($O(h)$).<br>• **Diferencias finitas centradas** ($O(h^2)$).<br>• Extrapolación de Richardson. | **Error de Truncamiento** (si el paso $h$ es grande) **en equilibrio con Error de Redondeo** (si $h$ es extremadamente pequeño ocurre *cancelación por resta* al hacer $f(x+h) - f(x)$). | • **Si predomina Truncamiento:** **Reducir el tamaño del paso ($h$)** o **usar fórmulas de mayor orden de exactitud (Diferencias Centradas $O(h^2)$** en vez de hacia adelante/atrás).<br>• **Si predomina Redondeo ($h$ muy chico):** Usar **doble precisión (`double`)** y no disminuir $h$ más allá del *punto de rendimientos decrecientes*. |
| **6. Integración numérica** *(Calcular el área bajo la curva o acumular $\int_a^b f(x)\,dx$)* | • **Fórmulas de Newton-Cotes:** Regla del Trapecio (simple o múltiple/compuesta), **Regla de Simpson 1/3**, **Regla de Simpson 3/8**.<br>• Integración de Romberg / Cuadratura de Gauss. | **Error de Truncamiento** *(por aproximar la curva real mediante segmentos rectos en Trapecio o parábolas/cúbicas en Simpson)*. | • **Aumentar el número de subintervalos/segmentos ($n$)**, lo que equivale a **disminuir el tamaño del paso ($h = \frac{b-a}{n}$)**.<br>• **Usar un método de orden superior** (ej. pasar de Regla del Trapecio $O(h^2)$ a **Regla de Simpson 1/3** $O(h^4)$). |
| **7. Ecuaciones Diferenciales Ordinarias (EDO)** *(Problemas de valor inicial: $\frac{dy}{dx} = f(x,y)$ con $y(x_0)=y_0$)* | • **Métodos de Runge-Kutta (1 paso):** **Método de Euler** ($O(h)$), **Método de Heun** (predictor-corrector, $O(h^2)$), Punto Medio, **Runge-Kutta de 4.º orden (RK4, $O(h^4)$)**.<br>• Métodos multipaso (Adams). | **Error de Truncamiento** *(compuesto por el error de truncamiento local en cada paso y el error de truncamiento propagado/global acumulado)*. | • **Disminuir el tamaño del paso ($h$)**.<br>• **Emplear un método de mayor orden de exactitud** (ej. cambiar de Euler a **Heun** o a **Runge-Kutta de 4.º orden RK4**, o usar paso adaptativo). |

---

## 2. 🕵️‍♂️ Cómo Identificar el "Tipo de Problema" en 5 Segundos según el Enunciado

Cuando leas el problema físico o matemático en el examen, buscá estas **palabras clave**:

1. **¿Te dan una ecuación y te piden hallar dónde se anula, el punto de equilibrio o despejar una variable que está adentro de un seno, exponencial o polinomio no lineal?**
   * 👉 **Tipo de problema:** **Raíces de ecuaciones** ($f(x) = 0$).
   * *Ejemplo clásico:* "Hallar la masa $m$ o el tiempo $t$ para el cual la velocidad alcanza cierto valor en $v(t) = \frac{gm}{c}(1 - e^{-(c/m)t})$", o "Hallar la profundidad $h$ de un tanque esférico".

2. **¿Te dan varias ecuaciones acopladas (ej. mallas de circuitos eléctricos con leyes de Kirchhoff, reactores conectados en estado estacionario o fuerzas en equilibrio estático) donde las incógnitas $x_1, x_2, x_3$ están multiplicadas por constantes?**
   * 👉 **Tipo de problema:** **Sistemas de ecuaciones algebraicas lineales** ($A \cdot x = b$).
   * *¡Ojo con la trampa del error acá!* Si el método elegido es **Eliminación de Gauss**, el único error que existe es el de **Redondeo** (porque Gauss no aproxima con series de Taylor, hace cuentas exactas en un número fijo de pasos).

3. **¿Te dan una tabla de puntos $(x_i, y_i)$ y te piden estimar cuánto vale la función en un punto $x$ que no está en la tabla?**
   * 👉 **Tipo de problema:** **Interpolación polinomial** (si los datos son precisos y la curva debe pasar exactamente por los puntos, usando **Lagrange o Newton**) o **Ajuste de curvas / Regresión** (si dice que son datos experimentales con ruido y pide hallar una tendencia).

4. **¿Te piden calcular una "tasa de cambio", "velocidad a partir de posiciones", "aceleración a partir de velocidades", "gradiente" o "flujo de calor $-k \frac{dT}{dx}$" en un punto específico?**
   * 👉 **Tipo de problema:** **Diferenciación numérica** (Diferencias finitas hacia adelante, atrás o centradas).

5. **¿Te piden calcular un "área", "volumen", "trabajo total ($\int F\,dx$)", "distancia total recorrida a partir de la velocidad ($\int v\,dt$)", "energía acumulada" o "masa total"?**
   * 👉 **Tipo de problema:** **Integración numérica** (Regla del Trapecio, Simpson 1/3, Simpson 3/8).

6. **¿Te dan una ecuación que tiene una derivada ($\frac{dy}{dt}$, $\frac{dv}{dt}$, $\frac{dT}{dt}$) junto con un valor inicial (ej. "en $t = 0$, la temperatura es $T(0) = 100$") y te piden saber cuánto valdrá la variable más adelante en el tiempo?**
   * 👉 **Tipo de problema:** **Ecuaciones Diferenciales Ordinarias (EDO - Problema de Valor Inicial)** (Euler, Heun, Runge-Kutta).

---

## 3. ⚡ Regla de Oro para las Preguntas 3 y 4 (Errores y Cómo Minimizarlos)

Si en el examen dudás entre **Error de Truncamiento** y **Error de Redondeo**, usá esta regla infalible de tu materia:

* **¿Cuándo la respuesta es ERROR DE REDONDEO?**
  1. En **Eliminación de Gauss / Gauss-Jordan / Descomposición $LU$** (métodos directos para sistemas lineales).
  2. Cuando el enunciado aclara específicamente que se está usando un **paso $h$ extremadamente diminuto** en diferenciación o que se están **restando dos números casi iguales** (cancelación por resta).
  * **¿Qué elegir para minimizarlo?** 👉 *"Usar mayor precisión en la representación numérica (precisión doble `double`)"*, *"Aplicar pivoteo parcial / escalamiento"* (si es Gauss), o *"Reformular la expresión para evitar restar números cercanos"*.

* **¿Cuándo la respuesta es ERROR DE TRUNCAMIENTO?**
  1. **En TODOS los demás métodos de la materia** (Bisección, Newton-Raphson, Secante, Gauss-Seidel, Interpolación de Lagrange/Newton, Diferenciación con paso normal, Trapecio, Simpson, Euler, Heun, Runge-Kutta) porque todos provienen de cortar la **Serie de Taylor** o cortar un proceso infinito.
  * **¿Qué elegir para minimizarlo?** 👉 
    * Si es un método **por pasos ($h$)** (Diferenciación, Trapecio, Simpson, Euler, RK): *"Disminuir el tamaño de paso $h$ (aumentar la cantidad de subintervalos $n$)"* o *"Utilizar un método de orden superior (más términos de Taylor)"*.
    * Si es un método **iterativo** (Bisección, Newton-Raphson, Secante, Gauss-Seidel): *"Aumentar el número de iteraciones / disminuir la tolerancia o criterio de parada ($e_s$)"*.
    * Si es **Interpolación** (Lagrange, Newton): *"Incluir más puntos (aumentar el grado del polinomio) o elegir puntos más cercanos al valor a interpolar"*.