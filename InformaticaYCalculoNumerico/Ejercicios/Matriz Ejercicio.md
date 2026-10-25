### 📝 Ejercicio de Matrices (Práctica antes de Cálculo Numérico)

Resolvamos este ejercicio en dos partes bien concretas:

**Parte A (Coordenadas rápidas):** Mirá la matriz de la diapositiva de tu clase (tiene 4 filas y 3 columnas):

```c++
int m[4][3] = {
    {-67,  29,  53},
    {-42,  10, -15},
    { 71, -76,  18},
    { 62, -33,   5}
};
```

1. ¿Qué número está guardado en la posición **`m[2][1]`**? -76
    
2. ¿Qué coordenadas **`m[?][?]`** tenés que escribir para acceder al número **`-15`**? `m[1][2]`
    

**Parte B (Seguimiento de un doble `for`):** Seguí este código que recorre una matriz chiquita de **2 filas por 2 columnas** y decime qué valores quedan en la matriz y cuánto vale `contador` al final:

```c++
#include <iostream>
using namespace std;

int main() 
{
    int mat[2][2] = {
        {4, 7},
        {2, 5}
    };
    int contador = 0; // contador=1, contador=2, contador=3 

    for (int i = 0; i < 2; i++) // i=1
    {
        for (int j = 0; j < 2; j++) // i=1,i=2,i=0,i=1
        {
            if (mat[i][j] > 3) 
            {
                contador = contador + 1;
            }
            mat[i][j] = mat[i][j] * 2; {8, 14}{4,10}
        }
    }

    cout << "Contador: " << contador << endl;
    cout << "Esquina inferior derecha: " << mat[1][1] << endl;
    return 0;
}
```

1. ¿Qué valor imprime en `"Contador: "`? (Fijate cuántos números de la matriz original eran mayores a `3` antes de ser multiplicados).  contador = 3
    
2. ¿Qué valor imprime en `"Esquina inferior derecha: "` (`mat[1][1]`) después de haber pasado por el doble ciclo `for`? `mat[1][1]`=10