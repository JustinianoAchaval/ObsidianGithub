#### 1. El ciclo `while` ("Mientras...")

Funciona muy parecido a un `if`, pero con una diferencia: cuando termina de ejecutar lo que está entre llaves `{}`, **vuelve a subir** y vuelve a preguntar si la condición sigue siendo verdadera. Repite el bloque una y otra vez **mientras** la condición sea verdadera, y recién sale cuando la condición se vuelve falsa.

Mirá este ejemplo paso a paso:

C++

```
#include <iostream>
using namespace std;

int main()
{
    int cuenta = 1;

    while (cuenta <= 3)
    {
        cout << "Vuelta numero: " << cuenta << endl;
        cuenta = cuenta + 1;
    }

    cout << "Termino el ciclo" << endl;
    return 0;
}
```

**¿Cómo lo ejecuta la computadora?**

1. `cuenta` arranca valiendo **`1`**.
    
2. Pregunta en el `while`: ¿`1 <= 3`? **Sí (Verdadero)**. Entra al ciclo: imprime `Vuelta numero: 1` y le suma 1 a `cuenta` (ahora `cuenta` vale **`2`**).
    
3. Sube de nuevo al `while`: ¿`2 <= 3`? **Sí**. Entra: imprime `Vuelta numero: 2` y suma 1 (`cuenta` vale **`3`**).
    
4. Sube de nuevo al `while`: ¿`3 <= 3`? **Sí**. Entra: imprime `Vuelta numero: 3` y suma 1 (`cuenta` vale **`4`**).
    
5. Sube de nuevo al `while`: ¿`4 <= 3`? **No (Falso)**. Sale del ciclo, sigue de largo hacia abajo e imprime `Termino el ciclo`.
    

> ⚠️ **¡Peligro: Ciclo Infinito!** Si adentro de las llaves `{}` del `while` te olvidás de poner `cuenta = cuenta + 1;` (o su atajo `cuenta++;`), `cuenta` va a valer `1` para siempre, la condición `1 <= 3` nunca va a dar falsa y el programa se va a quedar colgado imprimiendo infinitamente.


#### 2. El ciclo `for` (Repetición definida)

En tus diapositivas muestran que cualquier `while` con contador tiene 3 partes: **1) Inicializar el contador**, **2) Condición de corte**, y **3) Actualizar/incrementar el contador**. El ciclo **`for`** simplemente agrupa esas 3 cosas en un solo renglón entre paréntesis, separadas por punto y coma (`;`):

C++

```
for (int i = 0; i <= N; i++)
{
    sum += i;
}
```

- **`int i = 0;`** (Sentencia 1): Se ejecuta **una única vez** antes de arrancar el ciclo.
    
- **`i <= N;`** (Expresión): Es la condición; si da verdadera, entra a las llaves `{}`.
    
- **`i++`** (Sentencia 2): Se ejecuta **después** de terminar cada vuelta del cuerpo del ciclo (equivale a `i = i + 1`).

#### 3. El ciclo `do ... while` (Prueba posterior)

A diferencia de `while` y `for` (que preguntan la condición _antes_ de entrar), el **`do-while`** primero ejecuta el bloque y **pregunta la condición al final**.

- **¿Para qué sirve?** Garantiza que el cuerpo del ciclo se ejecute **al menos una vez**. Se usa mucho para pedirle un dato al usuario y validarlo (y se usa muchísimo en el método de Bisección en Cálculo Numérico):
    

C++

```
int n;
do 
{
    cout << "Ingrese un n (mayor que 1): ";
    cin >> n;
} while (n < 1);
```

(¡Ojo!: El `do-while` es el único ciclo que lleva un punto y coma `;` obligatorio después del paréntesis del `while`).

#### 4. ⚠️ ¡Fija de Parcial!: `break` vs `continue`

En las diapositivas de tu comisión analizan un mismo código cambiando `break` por `continue`. Mirá la diferencia:

- **`break` (Freno total):** Cuando el programa choca con un `break`, **rompe y termina el ciclo por completo** en ese mismo instante y salta a la primera línea que esté afuera de las llaves del ciclo.
    
- **`continue` (Saltear vuelta):** Cuando el programa choca con un `continue`, **no** rompe el ciclo; solamente **ignora las líneas que quedan abajo en esa vuelta**, sube directo al `i++` del `for` y pasa a la siguiente iteración.
    

Mirá el ejemplo de `break` de tu diapositiva:

C++

```
int N = 5;
for (int i = 0; i < N; i++)
{
    if (i == 3)
    {
        cout << "Condicion ";
        break;
    }
    cout << i << " ";
}
cout << "Fin";
```

- En las vueltas `0`, `1` y `2`, no entra al `if` e imprime: `0 1 2` .
    
- Cuando `i` llega a `3`, entra al `if`, imprime `Condicion` y el **`break`** mata el ciclo (nunca llega a imprimir el `3` ni hace la vuelta del `4`).
    
- Salta afuera e imprime `Fin`. Resultado en consola: **`0 1 2 Condicion Fin`**.