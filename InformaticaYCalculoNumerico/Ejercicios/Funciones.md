### 1. ¿Qué es conceptualmente una función?
ES _"un conjunto de instrucciones que cumplen una función específica y que potencialmente querría reutilizar en diferentes partes de un programa más grande"_ (como una receta de cocina donde le pasás los ingredientes y te devuelve la comida).

Toda función tiene 4 partes fundamentales (además del código de su cuerpo):

1. **Tipo de valor de retorno:** Qué devuelve la función (`int`, `float`, `double` o `void` si no devuelve nada).
2. **Nombre:** Para poder llamarla o invocarla.
3. **Parámetros Formales:** Las variables que recibe entre paréntesis.
4. **Valor de retorno (`return`):** El resultado final.


### 2. Pasaje por Valor vs. Pasaje por Referencia (`&`)

Esta es la "trampa" más grande en las pruebas de escritorio. En C++, hay dos formas de pasarle una variable a una función:

#### A) Pasaje normal (por valor)

Cuando le pasás una variable a una función, **C++ hace una copia** de ese valor en un espacio de memoria totalmente nuevo. Mirá este ejemplo de tu diapositiva:

```c++
void duplicar(int x) {
    x = x * 2;
    cout << "Dentro: " << x << endl;
}

int main() {
    int numero = 5;
    duplicar(numero);
    cout << "Fuera: " << numero << endl;
    return 0;
}
```

- **¿Qué pasa acá?** Se copia el `5` de `numero` adentro de `x`. La función multiplica su `x` por 2 (imprime `"Dentro: 10"`), pero la variable original `numero` allá en el `main()` jamás se enteró. Por lo tanto, imprime `"Fuera: 5"`.
    

#### B) Pasaje por Referencia (usando `&`)

Cuando agregamos el símbolo **`&`** al lado del tipo de dato en los parámetros de la función (ej. `int &x`), le estamos diciendo a C++ que **NO reserve un espacio de memoria nuevo** para hacer una copia. En lugar de eso, la función hace una "referencia" directa a la dirección de memoria de la variable original que le pasaste. Si cambias algo adentro de la función, **¡estás modificando la variable original!**

Mirá el mismo código de la diapositiva pero con el `&` agregado:

```c++
void duplicar(int &x) {
    x = x * 2;
    cout << "Dentro: " << x << endl;
}

int main() {
    int numero = 5;
    duplicar(numero);
    cout << "Fuera: " << numero << endl;
    return 0;
}
```

- **¿Qué pasa acá?** Al usar `int &x`, `x` se convierte en un "alias" o un cable directo hacia `numero`. Al multiplicar `x * 2`, está multiplicando el `numero` original. Va a imprimir `"Dentro: 10"` y también `"Fuera: 10"`.

### 3. 🚀 Arreglos (Arrays) y su gran excepción 

Un arreglo es una forma de guardar una lista de datos del mismo tipo bajo un solo nombre (como un vector en álgebra). Se declaran indicando el tamaño entre corchetes `[]`:

```c++
int numeros[4] = {10, 20, 30, 40};
```

- **Regla de oro de los índices:** En C++, ¡se empieza a contar desde cero!
    - `numeros[0]` vale `10`
    - `numeros[1]` vale `20`
    - `numeros[2]` vale `30`
    - `numeros[3]` vale `40`

#### ⚠️ La trampa de los arreglos en las funciones

En tus diapositivas hay un apartado específico que se llama _"¿Qué pasa con los arreglos como parámetro?"_. Recién vimos que para que una función modifique una variable normal hay que ponerle el `&`. **La gran excepción son los arreglos: cuando pasás un arreglo a una función, SIEMPRE se pasa por referencia de forma automática, sin necesidad de usar el `&`**.

Si modificás una posición del arreglo adentro de la función, ¡se modifica el arreglo original en el `main()`!

### 📦 ¿Cómo funciona un Arreglo en C++? (Modificar, Agregar y Quitar)

En C++, un arreglo básico (como `int numeros[4]`) **no es una lista flexible** a la que le podés estirar o achicar el tamaño mientras el programa corre. Imaginátelo como un **pastillero de plástico rígido con 4 casilleros numerados del 0 al 3**:

- Cuando escribís `int numeros[4] = {1, 2, 3, 4};`, la computadora reserva exactamente 4 "cajitas" pegadas en la memoria y ese tamaño queda fijo para toda la vida del arreglo:
    
    - Casillero `numeros[0]` $\rightarrow$ tiene el `1`
    - Casillero `numeros[1]` $\rightarrow$ tiene el `2`
    - Casillero `numeros[2]` $\rightarrow$ tiene el `3`
    - Casillero `numeros[3]` $\rightarrow$ tiene el `4`

#### 1. ¿Cómo se MODIFICA un valor?

Cada casillero individual (`numeros[0]`, `numeros[1]`, etc.) funciona exactamente igual que una variable común y corriente. Para cambiar lo que hay adentro, solo ponés el nombre del arreglo, el número de casillero entre corchetes `[ ]`, el signo `=` y el valor nuevo:

- Si escribís **`numeros[2] = 0;`**, vas al casillero de índice `2` (donde estaba el número `3`), tirás el `3` a la basura y guardás un **`0`** encima. Ahora el arreglo queda `{1, 2, 0, 4}`.
- Si escribís **`numeros[0] = numeros[0] + 10;`**, le sumás 10 al primer casillero (pasa de `1` a `11`).

_(Eso mismo era lo que hacía la línea `x[pos] = 0;` del ejercicio anterior: como `pos` valía `2`, hacía `x[2] = 0;`, sobrescribiendo el `3` con un `0`)_.

#### 2. ¿Cómo se "AGREGA" o carga información en un arreglo?

Como el pastillero es rígido y ya nace con sus 4 casilleros creados, **no se pueden agregar casilleros nuevos al final** (si declaraste tamaño 4, no existe `numeros[4]`). Lo que sí hacés en los programas es crear un arreglo vacío (por ejemplo, `double temp[5];`) e ir **llenando sus casilleros** uno por uno, ya sea a mano o usando un ciclo `for` con `cin >>`:

```c++
double temp[5];

// Llenamos los 5 casilleros (del 0 al 4) usando un ciclo for:
for (int i = 0; i < 5; i++) 
{
    cout << "Ingrese una temperatura: ";
    cin >> temp[i]; // Guarda el dato en el casillero 'i'
}
```

#### 3. ¿Cómo se "QUITA" un valor?

En los arreglos básicos de C++ (los que evalúan en tu parcial), **no se puede eliminar físicamente un casillero** porque la memoria reservada es fija. Si querés "borrar" o limpiar un dato en tus ejercicios de la materia, simplemente lo sobrescribís con un `0` (tal cual hacía la función `resetear` con `x[pos] = 0;`).

(Nota de color: El libro menciona al final del Capítulo 11 una herramienta avanzada llamada `vector` de la librería STL que sí permite estirar la lista con `.push_back()` o `.insert()`, pero en las diapositivas de tu cátedra y en Cálculo Numérico trabajan pura y exclusivamente con los **arreglos clásicos con corchetes `[]`** y ciclos `for`).