### 📝 Ejercicio 9 (Tu prueba de fuego para el parcial)

En los exámenes de tu materia les encanta mezclar los dos tipos de pasajes en la misma función para ver si caés en la trampa.

Hacé el seguimiento paso a paso de este código y decime **qué se va a imprimir en la pantalla exactamente** cuando llegue a los `cout` del `main()`:

```c++
#include <iostream>
using namespace std;

// La funcion recibe 'a' por valor (copia) y 'b' por referencia (cable directo)
void alterar(int a, int &b) {
    a = a + 10;
    b = b + 10;
}

int main() {
    int x = 5;
    int y = 5;
    
    alterar(x, y);
    
    cout << "x vale: " << x << endl;
    cout << "y vale: " << y << endl;
    
    return 0;
}
```

¿Qué valores quedan guardados e imprime al final para **`x`** y para **`y`**?  x = 5 y y = 15

### 📝 Ejercicio 10 (El último de C++ puro, sacado de tu clase)

Mirá este código exacto de tus diapositivas. Hacé el seguimiento e indicame qué va a mostrar en la pantalla (recordá cómo funcionan los índices que empiezan en `0` y la regla que acabamos de ver sobre arreglos en funciones):

```c++
#include <iostream>
using namespace std;

const int N = 4;

void resetear(int x[N], int pos) {
    x[pos] = 0;
    cout << "Dentro: " << x[pos] << endl;
}

int main() {
    int numeros[N] = {1, 2, 3, 4};
    
    resetear(numeros, 2);
    
    cout << "Fuera: " << numeros[2] << endl;
    return 0;
}
```

1. ¿Qué valor imprime en el `cout` de `"Dentro: "`?  0
    
2. ¿Qué valor imprime en el `cout` de `"Fuera: "`? 0 

### 📝 Ejercicio corto para ver si ahora sí quedó claro cómo manipularlos

Mirá este código donde creamos un arreglo de 3 casilleros y los vamos modificando usando sus índices entre corchetes `[ ]`:

```c++
#include <iostream>
using namespace std;

int main()
{
    int lista[3] = {10, 20, 30};

    lista[0] = 5;
    lista[2] = lista[0] + lista[1];

    cout << lista[0] << " - " << lista[1] << " - " << lista[2] << endl;
    return 0;
}
```

Seguí los casilleros (`lista[0]`, `lista[1]` y `lista[2]`):

1. ¿Qué número queda guardado en `lista[0]`?   5
    
2. ¿Cambió en algún momento `lista[1]` o cuánto vale? NO cambia de valor sigue siendo 20
    
3. ¿Qué número queda guardado en `lista[2]` después de hacer esa suma? 25
    
4. ¿Qué imprime el `cout` final? 5 - 20 - 25

### Simulacro Integrador de Programación C++ (Nivel Parcial)

Este ejercicio combina absolutamente todo lo que vimos en las Semanas 1 y 2: variables globales y locales, división entera vs. flotante, ciclos `for`, condicionales `if / else if / else`, `continue`, funciones con pasaje por valor, por referencia (`&`) y arreglos como parámetro.

Seguí el código con paciencia (podés anotar en un papel cómo van cambiando los valores) y respondé las preguntas de abajo:

```c++
#include <iostream>
using namespace std;

int global = 10;

void procesar(int a, int &b, int arr[], int tam) 
{
    a = a + 5; // a = 8 pero x = 3
    b = b + (global / 4); // b = y = 6
    global = global + 2; // global = 12

    for (int i = 0; i < tam; i++) // 0<3, 1<3, 2<3, 
    {
        if (i == 1) 
        {
            continue;
        }
        
        if (arr[i] % 2 == 0) 
        {
            arr[i] = arr[i] / 2; // datos[] = {4, 6, 5}
        } 
        else 
        {
            arr[i] = arr[i] + 1;
        }
    }
}

int main() 
{
    int x = 3;
    int y = 4;
    int datos[3] = {8, 6, 5};

    procesar(x, y, datos, 3);

    cout << "x: " << x << endl;
    cout << "y: " << y << endl;
    cout << "global: " << global << endl;
    cout << "arreglo: " << datos[0] << " - " << datos[1] << " - " << datos[2] << endl;

    return 0;
}
```

#### Tus desafíos para resolver:

1. **Valor de `x`:** ¿Qué imprime en `"x: "`? (Fijate cómo la recibe `a` en la función).
    
2. **Valor de `y`:** ¿Qué imprime en `"y: "`? (¡Cuidado con cuánto da la división entera `global / 4` cuando `global` vale `10`, y fijate que `b` tiene el `&`!).
    
3. **Valor de `global`:** ¿Con qué valor termina e imprime la variable `"global: "`?
    
4. **Valores del `arreglo`:** Seguí las 3 vueltas del ciclo `for` (`i = 0`, `i = 1`, `i = 2`) y decime cómo queda e imprime `"arreglo: "` (`datos[0] - datos[1] - datos[2]`). _(¡Ojo con lo que hace el `continue` cuando `i == 1`!)_.