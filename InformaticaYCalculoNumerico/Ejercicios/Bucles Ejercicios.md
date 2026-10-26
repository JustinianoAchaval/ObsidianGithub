### 📝 Ejercicio 7 (Tu primera prueba de escritorio con `while`)

Seguí este código vuelta por vuelta (como hice yo recién arriba) y respondé las dos preguntas:

C++

```c++
#include <iostream>
using namespace std;

int main()
{
    int x = 2;
    int suma = 0;

    while (x <= 6)
    {
        suma = suma + x; // 2 , 6, 12
        x = x + 2; // 4 , 6 , 8
    }

    cout << "Suma final: " << suma << endl;
    cout << "Valor final de x: " << x << endl;
    return 0;
}
```

1. ¿Cuántas vueltas (iteraciones) da el ciclo `while` en total? 3
    
2. ¿Qué valores imprime al final para **`suma`** y para **`x`**? (¡Ojo con qué valor queda `x` justo cuando logra escapar del `while`!). suma = 12 y x = 8


### 📝 Ejercicio 8 (El desafío de la diapositiva de tu clase)

Ahora hacé el ejercicio que sigue en la diapositiva: cambiamos el `break` por un **`continue`** y cambiamos un poquito el código:

C++

```
#include <iostream>
using namespace std;

int main()
{
    int N = 5;
    for (int i = 0; i < N; i++)
    {
        if (i == 2)
        {
            cout << "Salto ";
            continue;
        }
        cout << i << " ";
    }
    cout << "Fin";
    return 0;
}
```

**Preguntas:**

1. ¿Qué va a imprimir exactamente por consola este código de principio a fin? _(Prestá mucha atención a qué pasa cuando `i` vale `2` y choca con el `continue`: ¿imprime el número `2` abajo o pasa directo a la vuelta del `3`?)_.
	Va a imprimir 0, 1, Salto, 3, 4 y Fin 
    
2. Pregunta teórica corta del libro: Si tenés un ciclo `while (x > 10)` y otro `do { ... } while (x > 10);`, y antes de empezar `x` vale `5` (o sea, la condición ya es falsa de entrada): ¿cuántas veces se ejecuta el interior del `while` común y cuántas veces se ejecuta el interior del `do-while`?
	el while comun no se ejecuta nunca el do-while se ejecuta una vez