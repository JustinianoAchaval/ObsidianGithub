## 📘 BLOQUE 4: Ajuste de Curvas e Interpolación Polinomial

Cuando en ingeniería tenés una tabla de puntos $(x_i, y_i)$ obtenidos de mediciones o tablas, existen **dos estrategias distintas** según la calidad de los datos:

1. **Regresión por Mínimos Cuadrados (cuando los datos tienen "ruido" o error experimental):** No busca pasar por encima de cada punto, sino trazar **una única curva o recta que siga la tendencia general** del grupo minimizando la suma de los cuadrados de los residuos.
    
2. **Interpolación Polinomial (cuando los datos son exactos y confiables):** Busca construir el **único polinomio de grado $n$ (o menor) que pasa exactamente a través de los $n + 1$ puntos dados**:
    
    - Con **2 puntos** ($n=1$) $\rightarrow$ pasa una **recta** (polinomio de grado 1).
        
    - Con **3 puntos** ($n=2$) $\rightarrow$ pasa una **parábola** (polinomio de grado 2).
        
    - Con **$n + 1$ puntos** $\rightarrow$ pasa un polinomio de **grado $n$**.
        

> ⚠️ **Regla clave de parcial:** Aunque los métodos de **Newton** y **Lagrange** usan fórmulas y códigos distintos, **el polinomio interpolante que pasa por $n+1$ puntos es ÚNICO**, por lo que ambos métodos dan **exactamente el mismo resultado numérico**.

### 1. Polinomio de Interpolación de Newton en Diferencias Divididas

Armamos el polinomio agregando términos sucesivos (igual que en la Serie de Taylor):

$$f_n(x) = b_0 + b_1(x - x_0) + b_2(x - x_0)(x - x_1) + \dots + b_n(x - x_0)(x - x_1)\dots(x - x_{n-1})$$

- **¿Cómo se calculan los coeficientes $b_0, b_1, b_2$?** Usando una matriz llamada **Tabla de Diferencias Divididas (`fdd[N][N]`)**:
    
    - $b_0 = f(x_0)$ _(es directamente el primer valor $y_0$)_.
        
    - $b_1 = f[x_1, x_0] = \frac{f(x_1) - f(x_0)}{x_1 - x_0}$ _(primera diferencia dividida: pendiente entre punto 0 y 1)_.
        
    - $b_2 = f[x_2, x_1, x_0] = \frac{f[x_2, x_1] - f[x_1, x_0]}{x_2 - x_0}$ _(segunda diferencia dividida)_.
        

Mirá el código exacto de la diapositiva de tu **Clase 14 (`newton.cpp`)** que llena la matriz `fdd` con un doble `for` y luego evalúa el polinomio para un valor `consulta`:

C++

```
// 1. La columna 0 de la matriz se llena con los valores de y:
for (int i = 0; i < N; i++) {
    fdd[i][0] = y[i];
}

// 2. Se calculan las diferencias divididas columna por columna (j):
for (int j = 1; j < N; j++) {
    for (int i = 0; i < N - j; i++) {
        fdd[i][j] = (fdd[i + 1][j - 1] - fdd[i][j - 1]) / (x[i + j] - x[i]);
    }
}

// 3. Los coeficientes b0, b1, b2... quedan guardados en la Fila 0 (fdd[0][grado]):
double producto = 1.0;
aproximacion[0] = fdd[0][0];
for (int grado = 1; grado < N; grado++) {
    producto *= (consulta - x[grado - 1]);
    aproximacion[grado] = aproximacion[grado - 1] + fdd[0][grado] * producto;
}
```

- **¿Cuándo conviene usar Newton?** Cuando **no sabés de antemano qué grado usar** y querés ir probando grado 1, grado 2, grado 3... y comparar el error agregando puntos sin tener que recalcular todo desde cero.
    

### 2. Polinomio de Interpolación de Lagrange

No necesita crear ni guardar una matriz de diferencias divididas. Calcula directamente el valor interpolado sumando cada altura $y_i$ multiplicada por un "peso" o **polinomio base $L_i(x)$**:

$$f_n(x) = \sum_{i=0}^{n} L_i(x) \cdot y_i \quad \text{donde} \quad L_i(x) = \prod_{\substack{j=0 \\ j \neq i}}^{n} \frac{x - x_j}{x_i - x_j}$$

- **Propiedad de parcial de las bases $L_i(x)$:** Cada base $L_i(x)$ está diseñada con una condición mágica: **vale `1` cuando la evaluás en su propio nodo $x_i$, y vale `0` en todos los demás nodos $x_j$**. Así garantiza que la curva pase exactamente por $(x_i, y_i)$.
    
- **El código en C++ (de la Figura 18.11 de tu libro):** Usa un doble ciclo `for` con un **`if (i != j)`** para no dividir por cero (`xi - xi`):
    

C++

```
double suma = 0.0;
for (int i = 0; i < N; i++) 
{
    double producto = y[i];
    for (int j = 0; j < N; j++) 
    {
        if (i != j) 
        {
            producto = producto * (consulta - x[j]) / (x[i] - x[j]);
        }
    }
    suma = suma + producto;
}
```

- **¿Cuándo conviene usar Lagrange?** Cuando **el grado del polinomio ya se conoce de antemano (_a priori_)**, porque es muchísimo más corto y directo de programar que Newton.
    

_(Nota sobre **Trazadores o Splines Cúbicos**: Si tenés muchísimos puntos o datos con cambios bruscos, un solo polinomio de grado muy alto empieza a oscilar violentamente entre los puntos. Los **trazadores cúbicos** solucionan esto uniendo cada par de puntos con polinomios suaves de grado 3 igualando sus derivadas en los nodos de unión)._