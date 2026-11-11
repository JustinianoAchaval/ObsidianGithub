## 📘 BLOQUE 6: Ecuaciones Diferenciales Ordinarias (EDO - Valor Inicial)

En los bloques anteriores buscábamos un número $x$. En una EDO como $\frac{dy}{dx} = f(x, y)$ con una condición inicial conocida $(x_0, y_0)$ (por ejemplo, la velocidad del paracaidista $\frac{dv}{dt} = g - \frac{c}{m}v$), avanzamos paso a paso con un incremento $h$ usando la forma general:

$$\text{Nuevo valor } y_{i+1} = \text{Valor anterior } y_i + \text{Pendiente} \times h$$

Todos estos métodos pertenecen a la familia de métodos de un paso de **Runge-Kutta (RK)**:

### 1. Método de Euler (o RK de 1.er Orden)

Usa únicamente la derivada (pendiente) calculada al **inicio** del intervalo $(x_i, y_i)$ para saltar linealmente al punto siguiente:

$$y_{i+1} = y_i + f(x_i, y_i) \cdot h$$

- **En C++:** Adentro de un ciclo `while` o `for`, son solo dos líneas en cada paso:
    
    C++
    
    ```
    double dydx = funcion_derivada(x, y);
    y = y + dydx * h;
    x = x + h;
    ```
    
- **Limitación:** Tiene un error de truncamiento local de $O(h^2)$ y global de **$O(h)$**; si la función se curva rápido o el paso $h$ no es muy chico, acumula mucho error.
    

### 2. Método de Heun (Predictor-Corrector / RK de 2.º Orden)

Para no quedarse solo con la pendiente del principio como hace Euler, calcula el **promedio entre la pendiente del principio y la del final del paso** (igual que la regla del trapecio):

1. **Paso Predictor (Euler):** Predice un valor provisorio $y_{i+1}^0 = y_i + f(x_i, y_i) \cdot h$.
    
2. **Paso Corrector:** Usa ese valor provisorio para estimar la pendiente al final del intervalo $f(x_{i+1}, y_{i+1}^0)$ y corrige promediando ambas pendientes:
    
    $$y_{i+1} = y_i + \left[ \frac{f(x_i, y_i) + f(x_{i+1}, y_{i+1}^0)}{2} \right] \cdot h$$
    

### 3. Métodos de Runge-Kutta (RK) de Orden Superior (2.º, 3.º y 4.º Orden)

Logran la altísima exactitud de una Serie de Taylor de orden superior **sin necesidad de calcular derivadas segundas ni terceras a mano**, simplemente evaluando la función $f(x, y)$ en varios puntos intermedios (llamados $k_1, k_2, k_3, k_4$). El más famoso en ingeniería es **RK de 4.º orden (RK4)**, que tiene un error global pequeñísimo de **$O(h^4)$**:

$$y_{i+1} = y_i + \frac{1}{6}(k_1 + 2k_2 + 2k_3 + k_4) \cdot h$$