# Resumen de Integrales y Derivadas Clave

> **Nota personal:** Tabla de consulta rápida para no tener que calcular derivadas o integrales desde cero. Recordar siempre sumar la constante de integración ($C$) en las integrales indefinidas.

---

## 1. Propiedades Fundamentales

*   **Suma y Resta (Integrales):** $\int [f(x) \pm g(x)] dx = \int f(x) dx \pm \int g(x) dx$
*   **Constantes (Integrales):** $\int k \cdot f(x) dx = k \int f(x) dx$
*   **Suma y Resta (Derivadas):** $\frac{d}{dx} [f(x) \pm g(x)] = f'(x) \pm g'(x)$
*   **Constantes (Derivadas):** $\frac{d}{dx} [k \cdot f(x)] = k \cdot f'(x)$
*   **Producto (Derivadas):** $\frac{d}{dx} [f(x)g(x)] = f'(x)g(x) + f(x)g'(x)$
*   **Cociente (Derivadas):** $\frac{d}{dx} \left[ \frac{f(x)}{g(x)} \right] = \frac{f'(x)g(x) - f(x)g'(x)}{[g(x)]^2}$

---

## 2. Integrales Algebraicas y Exponenciales

| Función             | Integral                                | Condición         |
| :------------------ | :-------------------------------------- | :---------------- |
| **Constante**       | $\int a dx = ax + C$                    |                   |
| **Potencia**        | $\int x^n dx = \frac{x^{n+1}}{n+1} + C$ | $n \neq -1$       |
| **Inversa**         | $\int \frac{1}{x} dx = \ln\|x\| + C$    |                   |
| **Exponencial (e)** | $\int e^x dx = e^x + C$                 |                   |
| **Exponencial (a)** | $\int a^x dx = \frac{a^x}{\ln(a)} + C$  | $a > 0, a \neq 1$ |

---

## 3. Derivadas Algebraicas y Exponenciales

| Función | Derivada |
| :--- | :--- |
| **Constante** | $\frac{d}{dx} (a) = 0$ |
| **Variable** | $\frac{d}{dx} (x) = 1$ |
| **Potencia** | $\frac{d}{dx} (x^n) = n x^{n-1}$ |
| **Raíz Cuadrada** | $\frac{d}{dx} (\sqrt{x}) = \frac{1}{2\sqrt{x}}$ |
| **Exponencial (e)** | $\frac{d}{dx} (e^x) = e^x$ |
| **Exponencial (a)** | $\frac{d}{dx} (a^x) = a^x \ln(a)$ |
| **Logaritmo Natural** | $\frac{d}{dx} (\ln(x)) = \frac{1}{x}$ |

---

## 4. Integrales y Derivadas Trigonométricas

| Función Trigonométrica | Integral | Derivada |
| :--- | :--- | :--- |
| **Seno** | $\int \sin(x) dx = -\cos(x) + C$ | $\frac{d}{dx} (\sin(x)) = \cos(x)$ |
| **Coseno** | $\int \cos(x) dx = \sin(x) + C$ | $\frac{d}{dx} (\cos(x)) = -\sin(x)$ |
| **Tangente** | $\int \tan(x) dx = -\ln\|\cos(x)\| + C$ | $\frac{d}{dx} (\tan(x)) = \sec^2(x)$ |
| **Secante al cuadrado** | $\int \sec^2(x) dx = \tan(x) + C$ | N/A |

---

## 5. Métodos de Integración Salva-Papas

*   **Sustitución (Regla de la cadena inversa):** 
    Ideal cuando ves una función y su derivada multiplicándose.
    $$ \int f(g(x))g'(x)dx = \int f(u)du $$ 
    *(Donde $u = g(x)$ y $du = g'(x)dx$)*
*   **Integración por Partes (La regla de la vaca):**
    Para productos de funciones distintas (ej. un polinomio por una trigonométrica).
    $$ \int u dv = uv - \int v du $$
    *(Regla mnemotécnica ILATE para elegir $u$: Inversa, Logarítmica, Algebraica, Trigonométrica, Exponencial).*