### 🏗️ Desafío 1: ¿Qué es cada cosa? (Las cabeceras)

Tu objetivo es escribir **solamente la primera línea** (la cabecera) para definir estas tres estructuras. Tenés que decidir si llevan `public class`, `public abstract class`, `public interface`, `extends` o `implements`.

- **A) `Elemento3D`:** Es un concepto general. Sabemos que todos los elementos 3D tienen coordenadas X, Y, Z, pero el cálculo de su volumen depende de qué forma tengan. No queremos que nadie pueda hacer un `new Elemento3D()` genérico, porque no existe en la realidad. ¿Cómo definís su cabecera?
    
- **B) `Proyectable`:** Este es un "contrato" o comportamiento. Queremos que cualquier objeto que firme esto, esté obligado a tener métodos para generar sus vistas frontales y laterales en un plano 2D. No tiene variables, solo define reglas. ¿Cómo definís su cabecera?
    
- **C) `Cubo`:** Es un objeto real y concreto. Es un tipo de elemento 3D y, además, es capaz de proyectarse en vistas 2D. ¿Cómo definís la cabecera de esta clase vinculándola con las dos anteriores?
```Java
// A)
public abstract class Elemento3D {}  

// B)
public interface Proyectable {}

// C)
public class Cubo implements Elemento3D extends Proyectable {}
```

### ⚙️ Desafío 2: Las firmas de los métodos (¿void o tipo de dato?)

Ahora estamos trabajando **adentro** de la clase `Cubo`. Escribí **solamente la firma** (la primera línea) de estos tres métodos, decidiendo si llevan `public void`, `public int`, `public double`, etc.

- **A)** Un método llamado `cambiarColor` que recibe por paréntesis un texto (`String`) con el nuevo color. El método cambia el color del cubo internamente, pero no te tiene que devolver ninguna respuesta al terminar.
    
- **B)** Un método llamado `calcularVolumen` que no necesita recibir nada por paréntesis. Hace su matemática interna y te **devuelve** el resultado exacto del volumen (que puede tener números decimales).
    
- **C)** Un método abstracto llamado `renderizarMalla` que va a estar definido adentro del concepto general `Elemento3D`. No sabemos cómo se hace, obligamos a los hijos a hacerlo, y no queremos que devuelva nada. ¿Cómo se escribe esa firma abstracta?

```Java
// A)
public void cambiarColor(String color) {}

// B) 
public double calcularVolumen() {}

// C)
public abstract void renderizarMalla();
```

### 🕵️‍♂️ Desafío 3: El Detector de Mentiras

En el siguiente código hay **3 errores conceptuales graves** en las definiciones de clases e interfaces. ¿Te animás a marcarlos y decirme por qué están mal?

```Java
// Archivo 1
// Mal definido poner {} en el inferface
public interface Renderizable {
    public void limpiarPantalla() {
        System.out.println("Pantalla limpia");
    }
}

// Archivo 2
// no me doy cuenta 
public class Esfera implements Elemento3D {
    // codigo de la esfera
}

// Archivo 3
public abstract class Cilindro {
	// aca hace culaquier cosa, hace una definicion pero pone un ; 
    public abstract void girar();
}
// En el main alguien hace:
Cilindro miCilindro = new Cilindro();
```

