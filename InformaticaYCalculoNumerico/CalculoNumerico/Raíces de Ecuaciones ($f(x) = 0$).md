## 📘 BLOQUE 2: Raíces de Ecuaciones ($f(x) = 0$)

Buscar la **raíz** de una función $f(x)$ significa encontrar qué valor de $x$ hace que la cuenta dé exactamente **cero** ($f(x) = 0$), es decir, el punto donde la gráfica cruza el eje $X$. En tu materia los dividen en dos grandes familias: **Métodos Cerrados** y **Métodos Abiertos**.

### 1. Métodos Cerrados: Bisección y Falsa Posición (_Regula Falsi_)

Se llaman "cerrados" porque para arrancar necesitan **dos valores iniciales** ($x_l$ a la izquierda y $x_u$ a la derecha) que **encierren a la raíz** en el medio.

#### ¿Cómo sabe el programa que hay una raíz encerrada entre $x_l$ y $x_u$?

Por el **cambio de signo**: si de un lado la función está por debajo del eje $X$ (negativa) y del otro lado está por arriba (positiva), seguro cruzó por el cero en el medio. En C++, en vez de hacer dos preguntas largas, se multiplica **`f(xl) * f(xu)`**:

- Si **`f(xl) * f(xu) < 0`** (da negativo): tienen signos opuestos $\rightarrow$ **¡Hay raíz encerrada!**
    
- Si **`f(xl) * f(xu) > 0`** (da positivo): tienen el mismo signo $\rightarrow$ no se puede asegurar que haya raíz.
    

#### A) Método de Bisección (Cortar al medio)

En cada vuelta del ciclo `do-while` o `for`, el programa hace 3 pasos simples:

1. **Calcula el punto medio ($x_r$):**
    
    $$x_r = \frac{x_l + x_u}{2}$$
    
    _(En C++: `xr = (xl + xu) / 2.0;`)_.
    
2. **Elige con qué mitad quedarse (el `if-else` clave del parcial):** Evalúa el signo multiplicando **`f(xl) * f(xr)`**:
    
    - **Si `f(xl) * f(xr) < 0`:** La raíz quedó en la **mitad izquierda** (entre $x_l$ y $x_r$). Entonces el nuevo límite superior pasa a ser $x_r$: **`xu = xr;`**.
        
    - **Si `f(xl) * f(xr) > 0`:** La raíz quedó en la **mitad derecha** (entre $x_r$ y $x_u$). Entonces el nuevo límite inferior pasa a ser $x_r$: **`xl = xr;`**.
        
3. **Calcula el error $e_a$:** En bisección se puede usar la fórmula general $\left\vert{}\frac{x_r^{\text{nuevo}} - x_r^{\text{anterior}}}{x_r^{\text{nuevo}}}\right\vert{} \times 100$ o la fórmula exclusiva de bisección con los extremos: $e_a = \left\vert{}\frac{x_u - x_l}{x_u + x_l}\right\vert{} \times 100$.
    

> 💡 **Ventaja única de Bisección (Cálculo _a priori_ de iteraciones):** Es el único método donde podés saber **antes de empezar** cuántas vueltas ($n$) vas a necesitar para lograr un error absoluto deseado ($E_{a,d}$), porque el ancho del intervalo inicial ($\Delta x_0 = x_u - x_l$) se divide exactamente por $2$ en cada vuelta ($\frac{\Delta x_0}{2^n}$):
> 
> $$n = \frac{\log(\Delta x_0 / E_{a,d})}{\log(2)}$$

#### B) Método de la Falsa Posición (_Regula Falsi_)

Funciona con el mismo `if-else` de signos que Bisección, pero en lugar de cortar ciegamente a la mitad, **une los puntos $f(x_l)$ y $f(x_u)$ con una línea recta** y se fija dónde esa recta cruza el eje $X$:

$$x_r = x_u - \frac{f(x_u)(x_l - x_u)}{f(x_l) - f(x_u)}$$

- **Ventaja y Trampa de examen:** Casi siempre converge más rápido que Bisección, pero en funciones muy curvadas un extremo se queda "estancado", converge muy lento y el error aproximado $e_a$ engaña dando menor que el error verdadero ($e_a < e_t$).
    

### 2. Métodos Abiertos: Punto Fijo, Newton-Raphson y Secante

No necesitan encerrar la raíz en un intervalo; arrancan desde un único valor inicial $x_0$ (o dos en la secante) y "saltan" hacia la raíz. Si convergen, son **muchísimo más rápidos** que Bisección, pero corren el riesgo de **divergir** (alejarse al infinito).

|**Método**|**Fórmula Iterativa (xi+1x_{i+1}xi+1​)**|**Característica Clave y Peligros (Fijas de Parcial)**|
|---|---|---|
|**1. Punto Fijo**|Despejás $x$ de $f(x)=0$ para armar $x = g(x)$:<br><br>  <br><br>$$x_{i+1} = g(x_i)$$|Solo converge si la derivada de $g(x)$ cerca de la raíz es menor a 1 en valor absoluto (**$\vert{}g'(x)\vert{} < 1$**). Si $\vert{}g'(x)\vert{} > 1$, diverge.|
|**2. Newton-Raphson** _(El más famoso)_|Usa la recta tangente (necesita la derivada $f'(x)$):<br><br>  <br><br>$$x_{i+1} = x_i - \frac{f(x_i)}{f'(x_i)}$$|**Convergencia cuadrática** (el error nuevo es proporcional al cuadrado del error anterior: $E_{t,i+1} \propto E_{t,i}^2$, duplicando las cifras significativas en cada vuelta).<br><br>  <br><br>**Peligro:** Si la derivada **$f'(x_i) \approx 0$** (pendiente horizontal), ¡divide por cero y el método explota!|
|**3. Secante**|Si es difícil derivar $f'(x)$, reemplaza la derivada por una recta entre dos puntos ($x_{i-1}$ y $x_i$):<br><br>  <br><br>$$x_{i+1} = x_i - \frac{f(x_i)(x_{i-1} - x_i)}{f(x_{i-1}) - f(x_i)}$$|No necesita calcular derivadas, pero requiere **dos puntos iniciales** (sin necesidad de que encierren a la raíz). Si $f(x_{i-1}) \approx f(x_i)$, sufre de **cancelación por resta** en el denominador.|

### 📝 Práctica del Bloque 2 (3 ejercicios cortos de examen)

Resolvamos estos 3 puntos bien concretos (con cuentas redondas y fáciles) para poner a prueba Bisección y Newton-Raphson:

#### Ejercicio 1: Una vuelta de Bisección a mano

Querés encontrar la raíz de **$f(x) = x^2 - 9$** (sabemos que la raíz positiva es $3$) usando Bisección en el intervalo inicial **`xl = 0`** y **`xu = 4`**:

1. ¿Cuánto valen $f(0)$ y $f(4)$? ¿Se cumple que $f(x_l) \cdot f(x_u) < 0$?
    
2. **Iteración 1:** Calculás el punto medio $x_r = \frac{0 + 4}{2} = \mathbf{2}$. Evaluás la función ahí: ¿cuánto da **$f(2)$**?
    
3. Ahora el programa hace el `if`: multiplica **`f(xl) * f(xr)`** (o sea, $f(0) \cdot f(2)$). ¿Ese producto da positivo o negativo? Entonces, para la **Iteración 2**, ¿la raíz quedó entre $[0, 2]$ o entre $[2, 4]$? (¿Cuál sería el nuevo `xl` y el nuevo `xu`?).
    

#### Ejercicio 2: Una vuelta de Newton-Raphson en C++

Mirá este código en C++ que aplica Newton-Raphson para la misma función **$f(x) = x^2 - 9$**, cuya derivada es **$f'(x) = 2x$**:

```c++
double x = 5.0; // Valor inicial x0
double fx = x * x - 9.0;
double dfx = 2.0 * x;

double x_nuevo = x - (fx / dfx);
```

1. Si `x` arranca en `5.0`, ¿cuánto valen `fx` y `dfx`?
    
2. ¿Qué número exacto queda guardado en **`x_nuevo`** después de aplicar la fórmula `x - (fx / dfx)`? _(Fijate qué rápido se acerca al $3$ en un solo paso)._
    

#### Ejercicio 3: Pregunta tramposa de teoría

Si en el Ejercicio 2 el usuario hubiera elegido como valor inicial **`double x = 0.0;`** en Newton-Raphson para $f(x) = x^2 - 9$, ¿por qué fallaría catastróficamente el programa al intentar calcular `x_nuevo`?