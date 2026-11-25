## Punto 1: Representación matricial y operaciones elementales por filas

### 1. Definiciones formales

- **Expresión matricial de un SEL:** Un sistema de $m$ ecuaciones lineales con $n$ incógnitas se expresa como:
    $$A X = H$$
    
    donde $A \in \mathbb{R}^{m \times n}$ es la **matriz de coeficientes**, $X \in \mathbb{R}^{n \times 1}$ es la **matriz columna de incógnitas** y $H \in \mathbb{R}^{m \times 1}$ es la **matriz columna de términos independientes**.
    
- **Matriz ampliada:** Es la matriz $[A \mid H] \in \mathbb{R}^{m \times (n+1)}$ que se obtiene adjuntando la columna $H$ a la derecha de $A$.
    
- **Operaciones elementales por filas (OEF):** Dada una matriz $A \in \mathbb{R}^{m \times n}$, existen tres tipos, y **toda OEF admite una operación elemental inversa del mismo tipo**:
    
    - **Tipo I (Escalamiento):** Multiplicar la fila $i$ por un escalar $k \neq 0$ ($F_i \to kF_i$). Su inversa es $F_i \to k^{-1}F_i$.
        
    - **Tipo II (Combinación lineal):** Sumar a la fila $i$ un múltiplo escalar de otra fila $j$ ($F_i \to F_i + kF_j$, con $i \neq j$). Su inversa es $F_i \to F_i + (-k)F_j$.
        
    - **Tipo III (Permutación):** Intercambiar las filas $i$ y $j$ ($F_i \leftrightarrow F_j$). Es su propia inversa.
        
- **Matrices equivalentes por filas ($B \sim A$):** Dos matrices $A, B \in \mathbb{R}^{m \times n}$ son equivalentes por filas si $B$ se obtiene a partir de $A$ mediante una **cantidad finita** de operaciones elementales por filas. Esta relación es de equivalencia: cumple **reflexividad** ($A \sim A$), **simetría** ($B \sim A \implies A \sim B$) y **transitividad** ($A \sim B \land B \sim C \implies A \sim C$).
    
- **Matriz elemental ($E$):** Es toda matriz cuadrada $E \in \mathbb{R}^{m \times m}$ obtenida al aplicar **una única** operación elemental por filas $e$ a la matriz identidad $I_m$, es decir, $E = e(I_m)$.
    

### 2. Teoremas clave

1. **Invarianza del conjunto solución:** Si $[A' \mid H']$ se obtiene de $[A \mid H]$ mediante una operación elemental por filas (y por corolario, si $[A' \mid H'] \sim [A \mid H]$), entonces los sistemas $AX = H$ y $A'X = H'$ son **equivalentes**, es decir, tienen exactamente el mismo conjunto solución.
    
2. **Representación matricial de las OEF:** Si $e$ es una OEF y $E = e(I_m)$ es su matriz elemental asociada, entonces para toda matriz $A \in \mathbb{R}^{m \times n}$ se cumple que aplicar $e$ a $A$ equivale a **pre-multiplicar** $A$ por $E$:
    
    $$e(A) = E A$$
    
3. **Caracterización de la equivalencia por filas:** Sean $A, B \in \mathbb{R}^{m \times n}$. Entonces:
    
    $$B \sim A \iff \exists P \in \mathbb{R}^{m \times m} \text{ (producto finito de matrices elementales } P = E_k \cdots E_2 E_1\text{) tal que } B = PA$$
    

### 3. Posibles preguntas o demostraciones de examen final

- **Demostrar que $\sim$ es una relación de equivalencia** (la simetría se justifica usando la existencia de la operación elemental inversa aplicada en orden inverso).
    
- **Justificar por qué el orden de los factores en $P = E_k \cdots E_2 E_1$ es de derecha a izquierda:** al aplicar primero $e_1$ y luego $e_2$, se obtiene $e_2(e_1(A)) = E_2(E_1 A) = (E_2 E_1)A$.
    
- **Justificar por qué multiplicar una fila por $k = 0$ no es una OEF:** destruiría información de la ecuación (no tendría operación inversa) y podría agregar soluciones falsas al sistema.
    

### [Videos Bloque 1](Videos%20Bloque%201.md)
### Ejercicios estilo examen final — Punto 1

Resolvé estos dos puntos con la justificación que escribirías en el final y mandame tu respuesta para corregirla:

**Ejercicio 1 (Teórico / Demostración breve):**

Sea $AX = H$ un sistema de ecuaciones lineales con $A \in \mathbb{R}^{m \times n}$, y sea $E \in \mathbb{R}^{m \times m}$ la matriz elemental asociada a una operación elemental por filas $e$. Demostrá que los sistemas $AX = H$ y $(EA)X = EH$ tienen el mismo conjunto solución (recordá probar la doble inclusión: toda solución del primero es solución del segundo, y viceversa).

**Ejercicio 2 (Práctico con justificación):**

Dadas las matrices:

$$A = \begin{pmatrix} 1 & 2 & 0 \\ 2 & 5 & -1 \\ 0 & -1 & 3 \end{pmatrix} \quad \text{y} \quad B = \begin{pmatrix} 1 & 2 & 0 \\ 0 & 1 & -1 \\ 0 & 0 & 2 \end{pmatrix}$$

a) Indicá una secuencia de 2 operaciones elementales por filas ($e_1$ y $e_2$) que transforme $A$ en $B$.
F2 - 2.F1 despues F3 + F2

b) Escribí las matrices elementales $E_1$ y $E_2$ asociadas y calculá la matriz $P$ tal que $B = PA$.


c) Justificá teóricamente (sin calcular determinantes ni hacer cuentas) por qué $A$ también es equivalente por filas a $B$, y expresá $A$ en función de $B$ y las inversas de $E_1, E_2$.