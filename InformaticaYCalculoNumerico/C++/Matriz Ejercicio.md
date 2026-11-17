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

#### Ejercicio A: Diagonal, Transpuesta y Funciones

Mirá este código que recibe una matriz de $3 \times 3$ en una función (recordá que las matrices siempre se modifican en el original) y también recibe una variable por referencia (`&sumaDiag`):

```c++
#include <iostream>
using namespace std;

void transformar(int m[3][3], int &sumaDiag) 
{
    sumaDiag = 0; // 2, 7, 10
    for (int i = 0; i < 3; i++) // 1, 2
    {
        for (int j = 0; j < 3; j++) 
        {
            if (i == j) 
            {
                sumaDiag = sumaDiag + m[i][j];
            } 
            else if (i < j) 
            {
                m[i][j] = m[j][i]; 
            }
        }
    }
}

int main() 
{
    int mat[3][3] = {
        {2, 9, 8}, // {2, 4, 1}
        {4, 5, 7}, // {4, 5, 6}
        {1, 6, 3}  // {1, 6, 3}
    };
    int total = 100;

    transformar(mat, total);

    cout << "Total diagonal: " << total << endl;
    cout << "Fila 0: " << mat[0][0] << " " << mat[0][1] << " " << mat[0][2] << endl;
    cout << "Elemento [1][2]: " << mat[1][2] << endl;
    return 0;
}
```

**Preguntas del Ejercicio A:**

1. ¿Qué valor imprime en `"Total diagonal: "`? 7
    
2. Cuando el ciclo pasa por la Fila 0 (`i = 0`), para `j = 1` y `j = 2` se cumple que `i < j` y ejecuta `m[i][j] = m[j][i];`. ¿Qué 3 números imprime entonces en `"Fila 0: "`?  {2, 4, 1}
    
3. ¿Qué número queda guardado e imprime en `"Elemento [1][2]: "`? 6

#### Ejercicio : Suma de dos Matrices (Ejercicio 11.3 - Punto 4 del libro)


El libro pide escribir un programa que sume los elementos equivalentes de dos matrices llamadas `primero` y `segundo` (ambas de **2 filas y 3 columnas**) y guarde el resultado en una tercera matriz `resultado[2][3]`. Te dejo la base inicializada tal cual la da el libro para que vos escribas los ciclos `for` que hacen la suma y la muestran:

```c++
#include <iostream>
using namespace std;

int main() 
{
    int primero[2][3] = {{16, 18, 23}, {54, 91, 11}};
    int segundo[2][3] = {{24, 52, 77}, {16, 19, 59}};
    int resultado[2][3];

    // ESCRIBI ACA TU DOBLE FOR PARA CALCULAR resultado[i][j]
    // Y MOSTRARLO CON cout

    return 0;
}
```

(Pista: Adentro del doble `for`, cada casillero `resultado[i][j]` es la suma de `primero[i][j] + segundo[i][j]`).