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

1. ¿Qué número queda guardado en `lista[0]`? 
    
2. ¿Cambió en algún momento `lista[1]` o cuánto vale?
    
3. ¿Qué número queda guardado en `lista[2]` después de hacer esa suma?
    
4. ¿Qué imprime el `cout` final?