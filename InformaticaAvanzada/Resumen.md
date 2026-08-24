## ☕ Conceptos Clave de POO en Java (Para Finales)

### 1. Encapsulamiento y Modificadores de Acceso

Es el control de quién puede ver y modificar el estado interno de tus objetos. En los diagramas UML, estos permisos se indican con símbolos matemáticos.

- **`private` ( - ):** La regla de oro para los atributos/variables. Significa que solo la propia clase puede ver y tocar esa información. Desde afuera, el acceso se realiza exclusivamente a través de métodos `get` y `set`.
    
- **`public` ( + ):** Visible para todo el sistema. Se utiliza casi exclusivamente para los métodos, constructores y para la definición de la clase en sí.
    
- **`protected` ( # ):** Un punto medio estratégico. Visible para la propia clase, para otras clases en la misma carpeta (paquete), y **muy importante**: para todas las clases hijas que hereden de ella, sin importar dónde estén.
    
- **Sin modificador (Default):** Si no escribís ninguna palabra, la variable queda visible para cualquier archivo que esté en el mismo paquete. Omitir el `private` suele ser causa automática de desaprobación por romper el encapsulamiento.
    

### 2. El ADN vs. El Contrato (Herencia e Interfaces)

|**Característica**|**Herencia (extends)**|**Interfaz (implements)**|
|---|---|---|
|**Relación**|Es un "ADN". Define **qué es** el objeto de forma estructural.|Es un "Contrato". Define **qué sabe hacer** el objeto.|
|**Límite**|Java es estricto: solo se puede heredar de **UNA** clase padre.|Se pueden firmar **MÚLTIPLES** interfaces al mismo tiempo separadas por comas.|
|**Componentes**|Las clases abstractas pueden tener variables reales y métodos con código.|Las interfaces tradicionales solo tienen firmas de métodos vacíos (terminan en `;`).|

### 3. Enumerados (`enum`)

Una estructura especial que restringe las opciones a un grupo cerrado, fijo y predefinido de valores constantes.

- **Mecánica:** Se utilizan para representar conceptos limitados en la vida real que no cambian durante el uso del programa (ej: `TalleRopa`, `DiasSemana`, `EstadoDeAlarma`).
    
- **Uso estricto:** Como son valores estáticos, no se "fabrican" con la palabra `new`. Para asignarlos o compararlos, la sintaxis obligatoria siempre es `NombreDelEnum.VALOR_EXACTO`.
    
- **Seguridad:** Su principal ventaja es evitar errores humanos. Al usar un `enum`, es imposible que el programa reciba la palabra "Aereo" si el sistema estrictamente esperaba "AEREO".
    

### 4. Las 4 Palabras Reservadas Críticas

- **`this`:** Significa "este objeto exacto". Se usa para auto-referenciarse, especialmente útil para diferenciar el atributo global de la clase de un parámetro local que casualmente se llama igual (ej: `this.nombre = nombre;`).
    
- **`super`:** Significa "mi clase padre". Se usa cuando una clase hija necesita llamar obligatoriamente al constructor de su padre, o cuando quiere usar un método original del padre que el hijo acaba de sobrescribir.
    
- **`static`:** Hace que una variable o método pertenezca a **la clase entera** y no a un objeto individual. Por ejemplo, si una clase `Auto` tiene un atributo `static int cantidadRuedas = 4`, todos los millones de autos que crees van a compartir ese mismo `4` en la memoria.
    
- **`final`:** Es el candado definitivo de Java.
    
    - En una **variable**, la convierte en una constante matemática inmodificable.
        
    - En un **método**, prohíbe que las clases hijas lo sobrescriban.
        
    - En una **clase**, prohíbe completamente que tenga hijos (cancela el `extends`).

## 📚 Comparativa de Colecciones en Java

### 📊 Tabla de Referencia Rápida

| Característica            | `ArrayList`                            | `HashMap`                    | `TreeMap`                                   |
| ------------------------- | -------------------------------------- | ---------------------------- | ------------------------------------------- |
| **Estructura**            | Lista (Índice -> Valor)                | Diccionario (Clave -> Valor) | Diccionario (Clave -> Valor)                |
| **Orden**                 | Mantiene el orden de inserción         | Sin orden garantizado        | Ordenado por la Clave (Alfabético/Numérico) |
| **Duplicados**            | Permite valores duplicados             | No permite claves duplicadas | No permite claves duplicadas                |
| **Velocidad de Búsqueda** | Lenta (O(n)) excepto por índice (O(1)) | Súper rápida (O(1))          | Intermedia (O(log n))                       |
| **Valores `null`**        | Permite múltiples `null`               | Permite una clave `null`     | **NO** permite claves `null`                |

### 1. `ArrayList` (La lista dinámica)

Es un arreglo (array) tradicional potenciado que crece automáticamente en la memoria cuando te quedás sin espacio.

- **Mecánica:** Los datos se guardan secuencialmente. Accedés a ellos a través de su posición numérica (índice 0, 1, 2...).
    
- **Punto Fuerte:** Lectura instantánea si sabés en qué posición exacta está el dato (ej: `lista.get(5)`).
    
- **Punto Débil:** Inserciones y borrados lentos en el medio de la lista. Si borrás el elemento en la posición 1, tiene que reacomodar y "empujar" a todos los elementos que le siguen.
    
- **Cuándo usarlo:** Cuando necesitás guardar una lista de objetos en el orden exacto en que se agregaron y tu operación principal va a ser recorrerlos o leerlos.
    

### 2. `HashMap` (El diccionario caótico y veloz)

Es una estructura basada en pares de Clave-Valor. Utiliza una función matemática (Hash) para saber en qué espacio exacto de la memoria guardar cada elemento.

- **Mecánica:** Guardás y buscás a través de una clave única (ej: Patente -> Auto, DNI -> Persona).
    
- **Punto Fuerte:** Velocidad extrema. Buscar, insertar o borrar toma exactamente el mismo tiempo sin importar si la colección tiene 10 elementos o 10 millones.
    
- **Punto Débil:** Es impredecible visualmente. Los elementos se organizan según lo que dicte el algoritmo de la memoria, por lo que si imprimís la colección, el orden parecerá aleatorio.
    
- **Cuándo usarlo:** Cuando necesitás buscar datos específicos rápidamente por un identificador único y no te importa en absoluto el orden en que se guarden o se muestren.
    

### 3. `TreeMap` (El diccionario ordenado)

También almacena pares Clave-Valor, pero por debajo está construido sobre una estructura de árbol binario de búsqueda (Red-Black Tree).

- **Mecánica:** A medida que insertás elementos, el árbol compara las claves y las acomoda en sus ramas para mantener un orden perfecto.
    
- **Punto Fuerte:** Los datos están perpetuamente ordenados por su Clave (alfabética o numéricamente). Es la herramienta ideal si necesitás consultar rangos (ej: "traeme todos los registros entre la clave 10 y la 50") o el primer/último elemento.
    
- **Punto Débil:** Es más lento que el `HashMap` en las operaciones del día a día (insertar o borrar) porque tiene que hacer cálculos matemáticos para rebalancear el árbol cada vez que lo modificás.
    
- **Cuándo usarlo:** Cuando necesitás la búsqueda por identificador único, pero es un requisito innegociable que los datos estén ordenados para mostrarlos o recorrerlos.

## 🧩 Complemento de Colecciones y Estructuras en Java

### 1. La familia de los `Set` (Los Conjuntos Exclusivos)

A diferencia de las Listas (que aceptan todo), la interfaz `Set` representa un grupo de elementos donde **está estrictamente prohibido tener duplicados**.

- **`HashSet`:** Es el primo hermano del `HashMap`. Guarda elementos sueltos (sin clave) de forma ultra rápida (O(1)).
    
    - _Regla:_ No mantiene ningún orden lógico.
        
    - _Uso ideal:_ Cuando necesitás una bolsa de elementos únicos y querés saber rapidísimo si un elemento ya existe adentro (ej: una lista negra de usuarios bloqueados).
        
- **`TreeSet`:** Es el primo hermano del `TreeMap`. Guarda elementos únicos pero los acomoda automáticamente de menor a mayor o alfabéticamente.
    
    - _Regla:_ Es un poco más lento (O(log n)) y los elementos adentro deben saber cómo compararse entre sí (implementar la interfaz `Comparable`).
        
    - _Uso ideal:_ Cuando necesitás un ranking de puntajes sin empates, ordenado de mayor a menor de forma automática.
        

### 2. `LinkedList` (La lista de eslabones)

Es la gran rival del `ArrayList`. En lugar de ser un bloque contiguo de memoria, es una cadena de "nodos", donde cada nodo tiene su dato y una flecha que apunta al siguiente nodo.

- **Punto Fuerte:** Inserciones y borrados ultra rápidos (O(1)) si estás trabajando en las puntas (al principio o al final de la lista). No tiene que "empujar" a nadie, solo reacomoda las flechas.
    
- **Punto Débil:** Búsquedas muy lentas (O(n)). Si querés el elemento de la posición 1000, tiene que empezar desde el 0 y saltar flecha por flecha hasta llegar al 1000.
    
- **Uso ideal:** Para implementar Colas (el primero en llegar es el primero en salir, como en el supermercado) o Pilas (el último en llegar es el primero en salir, como el botón de "Deshacer" del teclado).
    

### 3. La trampa invisible: `equals()` y `hashCode()`

Si vas a crear tus propios objetos (ej: una clase `Auto`) y los vas a guardar en un `HashSet` o usarlos como clave en un `HashMap`, estás **obligado** a sobrescribir (`@Override`) estos dos métodos en tu clase.

- **¿Por qué?** Porque por defecto, Java compara la dirección de memoria. Si hacés dos autos con la misma patente `new Auto("AAA")` y `new Auto("AAA")`, Java piensa que son distintos porque son dos objetos separados.
    
- **¿Qué hacen?**
    
    - `equals()`: Le enseña a Java cuándo dos objetos tuyos son lógicamente iguales (ej: "si tienen la misma patente, son el mismo auto").
        
    - `hashCode()`: Le da a tu objeto un número de identificación matemático para que el `HashMap`/`HashSet` sepa en qué "cajón" guardarlo súper rápido.
        

### 📊 Resumen Visual: ¿Qué colección elijo?

| **Necesidad**                                             | **Estructura Recomendada** |
| --------------------------------------------------------- | -------------------------- |
| Quiero una lista simple y busco mucho por posición        | `ArrayList`                |
| Agrego/saco elementos todo el tiempo de las puntas        | `LinkedList`               |
| Necesito buscar rápido por una Clave única (Diccionario)  | `HashMap`                  |
| Diccionario, pero necesito que las claves estén ordenadas | `TreeMap`                  |
| Solo quiero guardar elementos, pero que NO se repitan     | `HashSet`                  |
| Elementos sin repetir y que además se ordenen solos       | `TreeSet`                  |