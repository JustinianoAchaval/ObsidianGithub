### 1. Estructura y las 4 palabras clave

Tal como muestran las diapositivas de tu comisión y el libro de la cátedra, el `switch` utiliza cuatro palabras clave (**`switch`**, **`case`**, **`break`** y **`default`**) con esta estructura:

```c++
switch (x) 
{
    case 0:
        cout << "Vale cero" << endl;
        break;
    case 1:
        cout << "Vale uno" << endl;
        break;
    case 2:
        cout << "Vale dos" << endl;
        break;
    default:
        cout << "Es otro numero" << endl;
        break;
}
```

- **`switch (expresión)`:** Evalúa la variable o expresión entre paréntesis para saber en qué lugar de la estructura debe entrar. **Regla obligatoria:** la expresión dentro del `switch` **debe dar un resultado entero (`int`) o un carácter (`char`)** (ya que C++ convierte internamente los caracteres a números enteros); si ponés un decimal (`float` o `double`) o una desigualdad como `x >= 10`, dará un error de compilación.
    
- **`case valor:`:** Etiqueta cada valor específico con el que se compara la expresión (equivale a preguntar `if (x == valor)`). **Atención a la sintaxis:** después del valor de cada `case` van **dos puntos (`:`)**, no punto y coma. Si usás letras (`char`), van entre comillas simples, como `case 'a':`.
    
- **`break;`:** Indica el final de ese `case` y provoca la **salida inmediata** de toda la estructura `switch`.
    
- **`default:`:** Es opcional y funciona exactamente igual que el último `else` de una cadena `if - else if`: se ejecuta únicamente si el valor de la expresión no coincidió con ninguno de los `case` anteriores. También lleva dos puntos (`:`).
    

### 2. ⚠️ La gran trampa de parcial: ¿Qué pasa si te olvidás el `break`?

El `case` solo marca el **punto de entrada**, pero una vez que el programa entra a un `case`, **ignora todas las demás etiquetas `case` de abajo y sigue ejecutando todas las líneas hacia abajo de corrido hasta chocar con un `break` o llegar a la llave de cierre `}`**.

Si omitís el `break`, ocurre un efecto cascada donde se ejecutan todos los casos siguientes (incluido el `default`). Sin embargo, como explica tu libro, esto a veces se usa a propósito para **"apilar" varios casos** que deben hacer exactamente lo mismo:

```c++
switch (numero) 
{
    case 1:
        cout << "Que tenga una buena manana\n";
        break;
    case 2:
        cout << "Que tenga un buen dia\n";
        break;
    case 3:
    case 4:
    case 5:
        cout << "Que tenga una buena tarde\n";
        break;
}
```

En este ejemplo del libro, si `numero` vale `3`, entra en `case 3:`, como no hay `break` sigue bajando por `case 4:` y `case 5:`, e imprime `"Que tenga una buena tarde"`.