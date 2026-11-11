## 📘 BLOQUE 3: Sistemas de Ecuaciones Lineales ($A \cdot x = b$) y Eliminación de Gauss

Ahora pasamos a cómo resuelve la computadora un sistema de varias ecuaciones con varias incógnitas usando **matrices**.

Imaginá este sistema de $2 \times 2$:

$$\begin{cases} 2x_0 + 3x_1 = 13 \\ 4x_0 + 10x_1 = 34 \end{cases}$$

En C++, los números que multiplican a las $x$ se guardan en la matriz **`A`** y los resultados de la derecha en el arreglo **`b`**.

El método de **Eliminación de Gauss Simple** consta de **2 fases**:

### Fase 1: Eliminación hacia adelante (Hacer ceros debajo de la diagonal)

El objetivo es transformar la matriz $A$ en una **matriz triangular superior** (que todo lo que esté debajo de la diagonal principal `A[i][i]` valga **cero**).

- Al elemento de la diagonal que usamos como referencia en cada paso (`A[k][k]`, por ejemplo el `2` de la primera fila) se lo llama **elemento pivote**.
    
- Para lograr que el `4` que está abajo del `2` se convierta en `0`, calculamos un `factor = A[i][k] / A[k][k]` (en nuestro ejemplo: `4 / 2 = 2`) y a la Fila 1 le restamos la Fila 0 multiplicada por ese `factor`:
    
    - Nueva Fila 1 de $A$: $(4 - 2 \times 2) = \mathbf{0}$ y $(10 - 2 \times 3) = \mathbf{4}$.
        
    - Nuevo $b[1]$: $(34 - 2 \times 13) = \mathbf{8}$.
        

Ahora el sistema quedó escalonado (triangular superior):

$$\begin{cases} 2x_0 + 3x_1 = 13 \\ 0x_0 + 4x_1 = 8 \end{cases}$$

### Fase 2: Sustitución hacia atrás (El código de tu diapositiva)

Una vez que tenés ceros abajo, despejás de **abajo hacia arriba** (empezando por la última fila `n - 1` y subiendo hasta la fila `0`). Mirá el código exacto que te dan en clase:

```c++
for (int i = n - 1; i >= 0; i--) {
    double suma = 0.0;
    for (int j = i + 1; j < n; j++) {
        suma = suma + A[i][j] * x[j];
    }
    x[i] = (b[i] - suma) / A[i][i];
}
```

1. **Primero despeja la última fila (`i = 1`):** Como abajo estaba $4x_1 = 8$, divide por el pivote `A[1][1]`: `x[1] = 8 / 4 = 2`.
    
2. **Después sube a la fila `i = 0`:** Pasa restando el término que ya conoce (`suma = A[0][1] * x[1] = 3 * 2 = 6`) y divide por el pivote `A[0][0]`: `x[0] = (13 - 6) / 2 = 3.5`.
    

### ⚠️ Las 3 Dificultades de Gauss y cómo se solucionan (¡Pregunta fija de parcial!)

En las diapositivas recalcan en naranja: **"Comprobar cada pivote, incluido el último"**. ¿Por qué? Porque Gauss simple falla en tres casos:

1. **División por cero (`A[i][i] == 0`):** Fijate que la última línea del código divide por **`A[i][i]`** (el pivote de la diagonal). Si en algún lugar de la diagonal aparece un `0`, ¡el programa divide por cero!
    
2. **Errores de redondeo (Pivote muy cercano a cero):** Si el pivote no es cero pero es un número diminuto (ej. `0.000001`), al dividir por él se amplifican brutalmente los errores de redondeo.
    
3. **Sistemas mal condicionados o singulares:** Un sistema es **singular** si no tiene solución única (dos filas son proporcionales y al escalonar queda toda una fila de ceros). Un sistema es **mal condicionado** cuando un cambio minúsculo en los datos de entrada provoca un cambio gigante en los resultados $x$.
    

> 💡 **¿Cómo se solucionan los puntos 1 y 2? Con PIVOTEO PARCIAL:**
> 
> Antes de eliminar una columna, el programa busca en esa columna (de la fila actual hacia abajo) cuál es el número más grande en valor absoluto (`abs()`) y **cambia de lugar (intercambia) toda esa fila** para poner al número más grande como pivote en la diagonal. Así evita dividir por cero y reduce el error de redondeo.

### 📝 Práctica del Bloque 3 (Sustitución hacia atrás y Pivoteo)

Resolvamos estos 2 ejercicios cortos usando el código de tu diapositiva:

#### Ejercicio 1: Seguimiento del código de Sustitución hacia atrás

Tenés un sistema de $2 \times 2$ (`n = 2`) que ya fue escalonado y quedó con estos datos en C++:

- **Fila 0:** `A[0][0] = 5`, `A[0][1] = 2`, y del otro lado del igual **`b[0] = 16`**
    
- **Fila 1:** `A[1][0] = 0`, `A[1][1] = 3`, y del otro lado del igual **`b[1] = 9`**
    

Seguí el código de tu diapositiva:

1. En la primera vuelta del `for` (`i = 1`), `suma` vale `0.0`. ¿Cuánto da **`x[1]`** al hacer `(b[1] - 0.0) / A[1][1]`?
    
2. En la segunda vuelta (`i = 0`), primero calcula `suma = A[0][1] * x[1]` (usando el `x[1]` que te dio en el punto 1) y luego hace `x[0] = (b[0] - suma) / A[0][0]`. ¿Cuánto vale **`suma`** y cuánto da finalmente **`x[0]`**?
    

#### Ejercicio 2: Pregunta práctica de Pivoteo Parcial

Mirá este sistema de ecuaciones antes de empezar Gauss:

- **Fila 0:** `0 * x0 + 4 * x1 = 8` (donde el pivote es `A[0][0] = 0`)
    
- **Fila 1:** `2 * x0 + 1 * x1 = 5`
    

1. ¿Por qué no podés aplicar Eliminación de Gauss simple directamente así como está ordenado?
    
2. ¿Qué haría la técnica de **Pivoteo Parcial** con la Fila 0 y la Fila 1 para arreglarlo?