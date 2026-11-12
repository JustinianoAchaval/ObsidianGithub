### Ejercicio 1: Impresión formateada y validación de límites

Codifique la definición de la función en C++:

`void mostrarTabla(double T[M][N], int n)`

que recibe como argumentos una matriz `T` de `M` filas y `N` columnas (con `N = 2`, donde la columna `0` almacena el **Tiempo (s)** y la columna `1` almacena la **Velocidad (m/s)**) y un entero `n` que indica cuántas filas mostrar.

- La función debe imprimir por pantalla los datos ubicados en las primeras `n` filas (siendo válido que `1 <= n <= M`), destinando **12 (doce) espacios** para cada número más **2 (dos) espacios adicionales** para separar las columnas.
    
- Debe imprimir el encabezado exacto: `Tiempo (s) Velocidad (m/s)` (con 3 espacios entre ambas palabras).
    
- En caso de que `n > M` o `n <= 0`, debe imprimir únicamente el cartel `"Error en cantidad de filas"` y no mostrar la tabla.
    

**Por ejemplo (suponiendo `M = 6`):**

|**Prueba**|**Resultado**|
|---|---|
|`mostrarTabla(Mediciones, 3);`|`Tiempo (s) Velocidad (m/s)`<br><br>  <br><br>`0 5.2`<br><br>  <br><br>`2 9.8`<br><br>  <br><br>`4 14.4`|
|`mostrarTabla(Mediciones, 8);`|`Error en cantidad de filas`|

```c++
#include <iostream>
using namespace std;

void mostrarTabla(double T[M][N], int n){
	if(n>M || n<=0){
		cout<<"Error en cantidad de filas"<<endl;
	} else {
		cout<<"Tiempo (s) Velocidad (m/s)"<<endl<<endl<<endl;
		for(i=0; i<n; i++){
			for(e=0; e<N; e++){
				cout<<setw(12)<<T[i][e]<<" ";
			}
			cout<<endl;
		}
	}

}
```


### Ejercicio 2: Cálculo numérico sobre la matriz (Aceleración / Derivada finita)

Codifique la definición de la función en C++:

`double calcularAceleracion(double T[M][N], int idx)`

que recibe la misma matriz `T[M][N]` de Tiempo (columna `0`) y Velocidad (columna `1`), y un índice de fila `idx`.

- La función debe calcular la **aceleración instantánea** ($a = \frac{dv}{dt}$) en la fila `idx` utilizando la fórmula de **diferencias finitas divididas centradas** entre la fila anterior (`idx - 1`) y la fila siguiente (`idx + 1`):
    $$a(t_{idx}) \approx \frac{v(t_{idx+1}) - v(t_{idx-1})}{t_{idx+1} - t_{idx-1}}$$
    
- **Validación:** Como la diferencia centrada necesita un vecino anterior y uno siguiente, los índices extremos (`0` y `M - 1`) o fuera de rango no son válidos. Si `idx <= 0` o `idx >= M - 1`, la función debe imprimir el texto `"Indice no valido para derivada centrada"` y devolver `-1.0`.
    

**Por ejemplo (con los mismos datos del Ejercicio 1, donde fila `0` es `(0, 5.2)`, fila `1` es `(2, 9.8)` y fila `2` es `(4, 14.4)`):**

|**Prueba**|**Resultado**|
|---|---|
|`double a = calcularAceleracion(Mediciones, 1);`<br><br>  <br><br>`cout << a << endl;`|`2.3`|
|`double a = calcularAceleracion(Mediciones, 0);`<br><br>  <br><br>`cout << a << endl;`|`Indice no valido para derivada centrada`<br><br>  <br><br>`-1`|
```c++
#include <iostream>
using namespace std;

double calcularAceleracion(double T[M][N], int idx){

}
```