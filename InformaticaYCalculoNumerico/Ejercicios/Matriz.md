### 1. ¿Qué es una Matriz en C++ y cómo se declara?

Si un arreglo común era una sola fila de casilleros, una **matriz (o arreglo bidimensional)** es una **tabla con filas y columnas** (como una planilla de Excel o un tablero de ajedrez). En tus diapositivas explican que cada fila es un arreglo, por lo que una matriz es simplemente un _"arreglo de arreglos"_.

Para declararla o acceder a un casillero, se usan **dos pares de corchetes `[fila][columna]`**:

- **El primer corchete SIEMPRE es la FILA** (`i`).
    
- **El segundo corchete SIEMPRE es la COLUMNA** (`j`).
    
- Igual que antes, tanto las filas como las columnas **empiezan a contarse desde el `0`**.

Mirá cómo se declara e inicializa una matriz de **3 filas y 4 columnas** según el libro de tu materia:

```c++
int val[3][4] = {
    {8, 16, 9, 52},
    {3, 15, 27, 6},
    {14, 25, 2, 10}
};
```

Si lo miramos como tabla con sus coordenadas `[fila][columna]`:

||**Columna 0**|**Columna 1**|**Columna 2**|**Columna 3**|
|---|---|---|---|---|
|**Fila 0**|`8` (`val[0][0]`)|`16` (`val[0][1]`)|`9` (`val[0][2]`)|`52` (`val[0][3]`)|
|**Fila 1**|`3` (`val[1][0]`)|`15` (`val[1][1]`)|`27` (`val[1][2]`)|`6` (`val[1][3]`)|
|**Fila 2**|`14` (`val[2][0]`)|`25` (`val[2][1]`)|`2` (`val[2][2]`)|`10` (`val[2][3]`)|

- Si querés leer o cambiar el número **`27`**, está en la **Fila 1, Columna 2**, así que escribís **`val[1][2]`**.
    
- Si escribís **`val[0][0] = 62;`**, el `8` de la esquina superior izquierda se borra y pasa a valer `62`.

### 2. ¿Cómo se recorre una matriz? (El doble ciclo `for` anidado)

Para recorrer un arreglo común usábamos un solo `for`. Para recorrer una matriz entera (por ejemplo, para cargarle datos con `cin`, mostrarla con `cout`, buscar un número o multiplicarla), tus diapositivas muestran que siempre se usan **dos ciclos `for` uno adentro del otro** (ciclos anidados):

- El `for` de afuera (con la variable **`i`**) va bajando **fila por fila**.
    
- El `for` de adentro (con la variable **`j`**) se mueve de izquierda a derecha por todas las **columnas de esa fila**.
    

Mirá los 3 esquemas clásicos que aparecen en las diapositivas de tu Comisión 5:

#### A) Modificar todos los elementos (ej. multiplicar toda la matriz por un número `k`)

```c++
for (int i = 0; i < N; i++) 
{
    for (int j = 0; j < M; j++) 
    {
        a[i][j] = a[i][j] * k;
    }
}
```
#### B) Contar cuántas veces aparece un valor `v` en la matriz

```c++
int res = 0;
for (int i = 0; i < N; i++) 
{
    for (int j = 0; j < M; j++) 
    {
        if (a[i][j] == v) 
        {
            res = res + 1;
        }
    }
}
```

#### C) Pasar una matriz a una función:

Igual que los arreglos de una dimensión, las matrices **se pasan automáticamente por referencia** (si la función cambia un casillero, cambia la matriz original). El único requisito de C++ es que en el encabezado de la función es obligatorio escribir cuántas columnas tiene entre el segundo corchete (ej. `void desplegar(int nums[FILAS][COLS])` o `void arr(int val[][COLS])`).

### Un detalle clave de tus diapositivas: Recorrer por Filas vs. por Columnas

En las diapositivas de tu materia muestran el ejemplo de una imagen de $8 \times 8$ píxeles (`imagen[FILAS][COLUMNAS]`) y comparan dos formas de usar el doble `for`:

- **Recorrido Fila por Fila (el estándar):** El ciclo de afuera mueve las filas (`i`) y el de adentro mueve las columnas (`j`). Completa toda la fila `0` de izquierda a derecha, luego baja a la fila `1`, y así sucesivamente:

```c++
    for (int i = 0; i < FILAS; i++) {
        for (int j = 0; j < COLUMNAS; j++) {
            cin >> imagen[i][j];
        }
    }
```

- **Recorrido Columna por Columna:** Si ponés primero el `for` de las columnas (`j`) afuera y el de las filas (`i`) adentro, pero adentro seguís escribiendo `imagen[i][j]`, el programa llena primero toda la columna `0` de arriba hacia abajo, luego toda la columna `1`, etc.:

```c++
    for (int j = 0; j < COLUMNAS; j++) {
        for (int i = 0; i < FILAS; i++) {
            cin >> imagen[i][j];
        }
    }
```

