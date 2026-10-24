Estructura inicial
```c++

#include <iostream>
using namespace std;

double main()

{

    double nota1 = 8.5;
    double nota2 = 9.5;
    double suma = nota1 + nota2;
    cout << suma << endl; //Imprime por pantalla 

    return 0;
}
```
### 📝 Ejercicio 2 (Sacado de la clase de tu materia)

Mirá este código numerado línea por línea tal cual aparece en tus apuntes:
``` c++
#include <iostream>
using namespace std;

int main()
 {
     int x = 1;
     int y = 0.2;
	y = x + 1;   
    int z = x + y;
	x = x + 1;
	x += 1;
 }
```
Hacé de "computadora" paso a paso de arriba hacia abajo y respondé estas 4 preguntas de la diapositiva:

1. ¿Qué valor almacena `x` después de ejecutar la **línea 6**? x = 1

2. ¿Qué valor almacena `y` después de ejecutar la **línea 7**? y = 0 ¿Y qué valor pasa a tener después de la **línea 8**? y = 2

3. ¿Qué valor tiene `z` después de ejecutar la **línea 9**? z = 3

4. ¿Con qué valor queda `x` en la **línea 10** y con qué valor termina finalmente en la **línea 11**? x =2 y x = 3

```c++
#include <iostream>
using namespace std;

int main()
{
    float I, V;
    cout << "Ingrese corriente y voltaje: ";
    cin >> I >> V; //Ingresa variables por teclado
    float P = I * V;
    cout << "La potencia es: " << P << endl; //Imprime La potencia es: P
    return 0;
}
```

Parte A (De la guía del libro): Sin usar compilador, calculá a mano qué número da cada una de estas tres expresiones en C++:

1. `15 / 4` = 3
    
2. `15 % 4` = 3
    
3. `15.0 / 4.0` = 3.75
    

**Parte B (Qué muestra este código):** Copiá o leé este código limpio y decime qué valores van a quedar guardados finalmente en `a`,
```c++
#include <iostream>
using namespace std;

int main()
{
    int a = 10 / 4;
    double b = 10 / 4;
    double c = 10.0 / 4.0;
    cout << a << " - " << b << " - " << c << endl;
    return 0;
}
```

**(Cadena `else if`):** Tomá como base una tabla de calificaciones del libro y escribí las líneas del `if - else if - else` para una variable `int nota`:

- Si `nota >= 90`, que imprima `"Excelente"`.
    
- Si no, si `nota >= 60`, que imprima `"Aprobado"`.
    
- Si no (para cualquier nota menor a 60), que imprima `"Desaprobado"`.
-
```c++
#include <iostream>
using namespace std; 

int main() {
	int nota = 0;
	cin >> nota; //No especifico que nota tiene asi que uso cin
	
	if (nota >= 90) {
		count << "Excelente" << endl;
	} if (nota<90 && nota >=60) {
		count <<"Aprobado" << endl; 
	} else {
		count << "Desaprobado" << endl;
	}
	return 0;
}
```

