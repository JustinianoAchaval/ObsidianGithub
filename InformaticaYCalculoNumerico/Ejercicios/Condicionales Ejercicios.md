### 📝 Ejercicio rápido de práctica (con trampa de `break`)

Seguí este código paso a paso y respondé las dos preguntas:

C++

```
#include <iostream>
using namespace std;

int main() 
{
    int opcion = 2;
    int total = 10;

    switch (opcion) 
    {
        case 1:
            total = total + 5;
            break;
        case 2:
            total = total + 10;
        case 3:
            total = total + 20;
            break;
        default:
            total = 0;
    }

    cout << "Total final: " << total << endl;
    return 0;
}
```

1. Sabiendo que `opcion` vale `2` y que **en el `case 2:` no hay un `break`**, ¿qué valor imprime exactamente en `"Total final: "`?
    
2. ¿Qué imprimiría en `"Total final: "` si al principio cambiáramos `int opcion = 2;` por `int opcion = 9;`?