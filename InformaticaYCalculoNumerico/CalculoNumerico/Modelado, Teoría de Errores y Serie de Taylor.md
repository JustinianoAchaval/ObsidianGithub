## 📘 BLOQUE 1: Modelado, Teoría de Errores y Serie de Taylor

### 1. Solución Analítica vs. Solución Numérica

- **Problema Físico $\rightarrow$ Modelo Matemático:** Para estudiar un fenómeno real (como la caída de un paracaidista frenado por el aire), se simplifica y formula un modelo matemático basado en leyes físicas (como la segunda ley de Newton).
    
- **Solución Exacta (Método Analítico):** Busca una expresión matemática cerrada. Tiene grandes limitaciones: solo funciona en modelos lineales, geometrías simples y problemas ideales; la mayoría de los problemas reales de ingeniería son no lineales e imposibles de despejar a mano.
    
- **Solución Aproximada:**
    
    - **Métodos Gráficos:** Sirven para explorar el problema, pero son tediosos y poco precisos.
        
    - **Métodos Numéricos:** Reformulan el problema matemático para resolverlo mediante **operaciones aritméticas básicas repetitivas** en una computadora. Dan excelentes aproximaciones con rapidez y permiten abordar problemas complejos.
        

### 2. Cifras Significativas, Exactitud y Precisión

- **Cifras (o dígitos) significativas:** Son los dígitos de un número que se conocen con certeza más **un último dígito estimado** (redondeado). Comienzan en el primer dígito distinto de cero a la izquierda y terminan en el último dígito confiable a la derecha.
    
    - _Ejemplo de tu clase:_ El número `87324.45` tiene **7 dígitos significativos** (los primeros 6 son certeros y el `5` final fue redondeado).
        
- **Exactitud vs. Precisión:**
    
    - **Exactitud:** Qué tan cerca está el valor calculado o medido del **valor verdadero**.
        
    - **Precisión:** Qué tan cerca están los valores calculados unos de otros (repetibilidad) o qué **cantidad de cifras significativas** (decimales) tiene un número en la computadora.
        
- **Trampa de C++ en tu diapositiva (`cout.precision`):** Usar `cout.precision` o `setprecision(n)` solo cambia **cuántos decimales se muestran en pantalla**, pero **NO cambia la precisión real de las operaciones** en la memoria. Para tener más precisión real en los cálculos, tenés que cambiar el tipo de variable de precisión simple (`float`, ~7 cifras significativas) a **precisión doble (`double`)** (64 bits, ~15-16 cifras significativas).
    

### 3. Los Componentes del Error Numérico Total

El **Error Numérico Total** es la suma de dos tipos de errores opuestos:

| **Tipo de Error**            | **¿Por qué ocurre?**                                                                                                                                                                                                 | **¿Cómo se reduce?**                                                                                                                                                                        |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. Error de Redondeo**     | Porque la computadora trabaja en binario (base 2) y tiene un límite físico de bits en la memoria. No puede guardar infinitos decimales (como en $\pi$ o $e$), por lo que "corta" o "redondea" la mantisa del número. | Usando variables de **doble precisión (`double`)**, evitando restar números casi iguales (**cancelación por resta**) y sumando series desde los números más pequeños hacia los más grandes. |
| **2. Error de Truncamiento** | Porque reemplazamos una expresión matemática exacta o infinita (como una derivada o una serie infinita) por una **fórmula aproximada finita**.                                                                       | **Reduciendo el tamaño del paso ($h$)** o agregando **más términos** al polinomio (por ejemplo, en la Serie de Taylor).                                                                     |

#### ⚠️ Dos conceptos teóricos de examen sobre estos errores:

1. **Cancelación por resta (Error de redondeo crítico):** Ocurre cuando el programa **resta dos números de punto flotante que son casi iguales** (por ejemplo, `0.7642 - 0.7641 = 0.0001`, o en la fórmula cuadrática $\frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$ cuando $b^2$ es muchísimo más grande que $4ac$). Se pierden de golpe casi todas las cifras significativas confiables.
    
2. **La paradoja del Error Total (El "Punto de rendimientos decrecientes"):** Si para achicar el **error de truncamiento** hacés que el tamaño del paso $h$ sea cada vez más chiquito, obligás a la computadora a hacer millones de cálculos más y a restar números muy cercanos. Llega un punto (llamado _punto de regreso disminuido_ o _de rendimientos decrecientes_) donde el **error de redondeo** crece tanto que empieza a dominar y el error total vuelve a subir (Figura 4.8 del libro).
    

### 4. Serie de Taylor y Orden del Error $O(h^{n+1})$

Es la herramienta matemática principal para predecir el valor de una función en un punto futuro $f(x_{i+1})$ a partir de su valor actual $f(x_i)$ y sus derivadas, dando un paso de tamaño $h = x_{i+1} - x_i$:

$$f(x_{i+1}) = f(x_i) + f'(x_i)h + \frac{f''(x_i)}{2!}h^2 + \frac{f^{(3)}(x_i)}{3!}h^3 + \dots + \frac{f^{(n)}(x_i)}{n!}h^n + R_n$$

- **¿Qué es $R_n$?** Es el **residuo o término de error de truncamiento** por haber cortado la serie en el grado $n$:
    
    $$R_n = \frac{f^{(n+1)}(\xi)}{(n+1)!}h^{n+1} = O(h^{n+1})$$
    
- **¿Qué significa que un método tenga error de orden $O(h)$ u $O(h^2)$?**
    
    - Si el error es de orden **$O(h)$** (proporcional a $h^1$) y reducís el paso $h$ **a la mitad** ($\frac{1}{2}$), el error de truncamiento se reduce **a la mitad**.
        
    - Si el error es de orden **$O(h^2)$** (proporcional a $h^2$) y reducís el paso $h$ **a la mitad** ($\frac{1}{2}$), el error se reduce a **una cuarta parte** ($(\frac{1}{2})^2 = \frac{1}{4}$).
        

### 5. Las Fórmulas para Medir el Error en tus Programas

1. **Error Verdadero ($E_t$) y Relativo Verdadero ($e_t$ o $e_v$):** Solo se puede calcular cuando conocés la respuesta exacta analítica:
    
    $$E_t = \text{Valor Verdadero} - \text{Aproximación}$$
    
    $$e_t (\%) = \left\vert{} \frac{\text{Valor Verdadero} - \text{Aproximación}}{\text{Valor Verdadero}} \right\vert{} \times 100$$
    
2. **Error Relativo Aproximado ($e_a$):** Es el que se programa adentro de los ciclos (`while` / `do-while`) cuando **no** conocemos el valor exacto, comparando la aproximación actual contra la de la iteración anterior:
    
    $$e_a (\%) = \left| \frac{\text{Aproximación Actual} - \text{Aproximación Anterior}}{\text{Aproximación Actual}} \right| \times 100$$
    
    El ciclo se detiene cuando se cumple que **$e_a \le e_s$** (donde $e_s$ es el error aceptable o tolerancia fijada).
    

### 📝 Práctica del Bloque 1 (4 preguntas cortas estilo parcial)

Respondé estas 4 preguntas rápidas para asegurar el Bloque 1 y pasar directo al **Bloque 2 (Raíces: Bisección y Newton-Raphson)**:

1. **Cálculo de error iterativo ($e_a$ y corte):** Estás corriendo un método iterativo con una tolerancia aceptable de **`es = 2.0` (2%)**. En la vuelta anterior obtuviste `x_anterior = 7.5` y en la vuelta actual obtuviste **`x_actual = 8.0`**.
    
    - ¿Cuánto da el error relativo aproximado porcentual $e_a$ haciendo $\left\vert{}\frac{8.0 - 7.5}{8.0}\right\vert{} \times 100$?
	    6.25
    - ¿El ciclo se detiene en esta vuelta o tiene que seguir iterando?
        tiene que seguir iterando por lo menos dos veces mas
1. **Serie de Taylor (Orden del error):** Estás usando un método numérico cuyo error de truncamiento es de orden **$O(h^2)$**. Si decidís achicar el tamaño del paso $h$ a la **mitad** (de $h = 0.4$ a $h = 0.2$), ¿el error se reduce a la mitad o a la cuarta parte?
	    a una cuarta parte
2. **Teoría de Errores:** Si estás programando la serie exponencial $e^x \approx 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!}$ en C++ y decidís cortar la fórmula ahí en $x^3$ sin sumar $x^4, x^5, \dots$, ¿ese error que estás cometiendo por cortar la fórmula matemática se llama **error de redondeo** o **error de truncamiento**?
	    error de truncamiento
3. **Trampa de C++ (de las diapositivas):** Si un compañero tiene un programa con variables `float` que le da mucho error de redondeo y, para solucionarlo, le agrega `cout.precision(12);` antes de mostrar el resultado: ¿logró mejorar la precisión del cálculo matemático o qué hizo realmente?
		solo cambia cuantos decimales se muestran por pantalla 