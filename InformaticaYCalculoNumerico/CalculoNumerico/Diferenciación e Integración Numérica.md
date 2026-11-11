## 📘 BLOQUE 5: Diferenciación e Integración Numérica

### 1. Diferenciación Numérica (Estimación de la derivada $f'(x)$)

Como vimos en tus diapositivas de la Clase 1, derivar numéricamente en un punto $x_i$ consiste simplemente en elegir dos puntos, **restar sus alturas y dividir por la separación $h$ entre ellos**:

|**Fórmula de Primera Derivada**|**Ecuación Matemática**|**Orden del Error de Truncamiento**|
|---|---|---|
|**1. Hacia adelante** _(usa el vecino derecho $x_{i+1}$)_|$$f'(x_i) \approx \frac{f(x_{i+1}) - f(x_i)}{h}$$|**$O(h)$** _(poco preciso)_|
|**2. Hacia atrás** _(usa el vecino izquierdo $x_{i-1}$)_|$$f'(x_i) \approx \frac{f(x_i) - f(x_{i-1})}{h}$$|**$O(h)$** _(poco preciso)_|
|**3. Centrada** _(usa ambos vecinos, $x_{i+1}$ y $x_{i-1}$)_|$$f'(x_i) \approx \frac{f(x_{i+1}) - f(x_{i-1})}{2h}$$|**$O(h^2)$** _(¡Mucho más exacta! Al restar Taylor hacia adelante y hacia atrás se cancelan los errores de primer orden)_|

### 2. Integración Numérica (Fórmulas de Newton-Cotes)

Integrar $\int_a^b f(x)\,dx$ significa calcular el **área bajo la curva** entre $a$ y $b$. Dividimos el intervalo $[a, b]$ en **$n$ subintervalos (paneles o segmentos)** de igual ancho **$h = \frac{b - a}{n}$** (notá que si hay $n$ subintervalos, la tabla tiene **$n + 1$ puntos**).

#### A) Regla del Trapecio (Une los puntos con rectas - Grado 1)

- **Un solo trapecio ($n = 1$):** $I \approx h \cdot \frac{f(a) + f(b)}{2}$.
    
- **Trapecio Compuesto ($n$ paneles - El código de tu Clase 3):** Los extremos $f(a)$ y $f(b)$ se suman **una sola vez**, pero todos los puntos interiores se multiplican **por `2`** porque cada pared interior es compartida por dos trapecios vecinos:
    
    $$I \approx \frac{h}{2} \left[ f(x_0) + 2\sum_{i=1}^{n-1} f(x_i) + f(x_n) \right]$$
    

Mirá el código exacto de tus diapositivas (**Clase 3**, basado en `TrapEq`):

C++

```
double h = (b - a) / n;
double x = a;
double suma = funcion(a);

for (int i = 1; i <= n - 1; i++) 
{
    x = x + h;
    suma = suma + 2.0 * funcion(x);
}

suma = suma + funcion(b);
double area = h * suma / 2.0;
```

#### B) Reglas de Simpson (Unen los puntos con curvas - Mayor exactitud)

En lugar de rectas, usan parábolas o cúbicas:

1. **Regla de Simpson 1/3:** Ajusta una parábola (grado 2) cada 3 puntos (2 paneles):
    
    $$I \approx \frac{h}{3} \left[ f(x_0) + 4f(x_1) + f(x_2) \right]$$
    
    - **Requisito obligatorio de parcial:** En su versión múltiple, **SOLO se puede aplicar si el número de segmentos $n$ es PAR** (los puntos impares se multiplican por `4` y los pares interiores por `2`).
        
    - **Exactitud extra:** Aunque se deduce con parábolas (grado 2), da resultados **100% exactos incluso para polinomios cúbicos (grado 3)** porque su error depende de la derivada cuarta $f^{(4)}(\xi)$ y su error global es $O(h^4)$.
        
2. **Regla de Simpson 3/8:** Ajusta un polinomio cúbico cada 4 puntos (**3 segmentos**):
    
    $$I \approx \frac{3h}{8} \left[ f(x_0) + 3f(x_1) + 3f(x_2) + f(x_3) \right]$$
    
    - **¿Para qué se usa en los programas?** Cuando tenés una cantidad **IMPAR** de segmentos: aplicás Simpson 3/8 en los últimos 3 segmentos y Simpson 1/3 en todos los demás segmentos pares anteriores.