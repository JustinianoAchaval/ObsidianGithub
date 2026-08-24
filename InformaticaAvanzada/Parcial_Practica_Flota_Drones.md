# Parcial de Práctica – Programación Orientada a Objetos (Java)

## Sistema de Gestión de una Flota de Drones de Reparto

Se desea modelar el sistema de control de una flota de drones de reparto. Cada **ruta** de reparto agrupa varios **drones**, cuenta con una **estación de carga** asociada, un **estado actual** y **monitores** que deben ser notificados cuando ocurre un cambio relevante en la ruta.

El sistema debe permitir: conocer el nivel de batería más crítico de una ruta, ordenar los drones según su batería, decidir si la ruta debe recargarse o entrar en emergencia, notificar eventos y administrar varias rutas desde un controlador general.

Se presenta el diagrama de clases general, que va a implementarse (parcialmente, y con variantes) en cada una de las preguntas del examen.

```
                        ControladorFlota
                        --------------------------
                        -rutas: HashMap<String, Ruta>
                        --------------------------
                        +ejecutarCicloControl(): void
                        +listarRutasEnEmergencia(): List<String>
                                   |
                                   | 1
                                   v *
                                 Ruta
                    -------------------------------------
                    -nombre: String
                    -drones: ArrayList<Dron>
                    -observadores: HashSet<Monitor>
                    -estacion: EstacionCarga
                    -estado: EstadoRuta
                    -------------------------------------
                    +obtenerBateriaMinima(): double
                    +ordenarDronesPorBateria(): void
                    +actualizarEstado(): void
                      |1        |1              |1
                      v*        v               v
      <<abstract>> Vehiculo   <<interface>> Monitor    <<interface>> EstadoRuta
      -------------------     ----------------------   --------------------------
      -id: String              +notificar(ruta: Ruta,   +ejecutar(ruta: Ruta): void
      -modelo: String            mensaje: String): void +getNombre(): EstadoZona
      -bateria: double                  ^                     ^    ^     ^
      +obtenerEstadoBateria()           |                     |    |     |
      {abstract}                    AppCentral        EstadoOperativa EstadoAlerta EstadoEmergencia
            ^          ^
            |          |
          Dron    EstacionCarga                          <<enum>> EstadoZona
    (implements       -capacidadMaxima: int                OPERATIVA
     Comparable<Dron>) -dronesEnCarga: ArrayList<Dron>      ALERTA
    -capacidadCarga: kg +recargarTodos(): void              EMERGENCIA
                                                             FUERA_DE_SERVICIO

        FlotaException  --------->  Exception
        (posee además un atributo "codigo: int")
```

---

### Pregunta 1 — Diagrama general (lectura)

No requiere código. Es el diagrama que se toma como referencia a lo largo del parcial (arriba).

---

### Pregunta 2 — Clase `Dron` (herencia + `Comparable`)

Considere el siguiente diagrama reducido:

```
                <<abstract>> Vehiculo
                ---------------------------------------
                -id: String
                -modelo: String
                -bateria: double
                ---------------------------------------
                +Vehiculo(id: String, modelo: String, bateria: double)
                +getId(): String
                +getModelo(): String
                +getBateria(): double
                +setBateria(bateria: double): void
                +obtenerEstadoBateria(): String {abstract}
                            ^
                            |
                          Dron  (implements Comparable<Dron>)
                ---------------------------------------
                -capacidadCarga: double
                ---------------------------------------
                +Dron(id: String, modelo: String, bateria: double, capacidadCarga: double)
                +getCapacidadCarga(): double
                +obtenerEstadoBateria(): String
                +compareTo(otro: Dron): int
```

A diferencia de un sensor pasivo, un `Dron` **no solo hereda** de `Vehiculo`, sino que además implementa `Comparable<Dron>` para poder ordenarse por nivel de batería (de menor a mayor).

Complete:

1. El constructor de `Dron`, que debe invocar al constructor de `Vehiculo`.
2. `getCapacidadCarga()`.
3. `obtenerEstadoBateria()`: debe devolver el texto `"Batería: X%"` (por ejemplo `"Batería: 45.0%"`), sobrescribiendo el método abstracto de `Vehiculo`.
4. `compareTo(Dron otro)`: debe permitir ordenar drones de menor a mayor batería (usar `Double.compare`).

**Por ejemplo:**

| Prueba | Resultado |
|---|---|
| `System.out.println("TEST constructor y orden");`<br>`Dron d1 = new Dron("D1","Delivery-X", 80.0, 2.5);`<br>`Dron d2 = new Dron("D2","Delivery-X", 30.0, 2.5);`<br><br>`System.out.println(d1.obtenerEstadoBateria());`<br>`System.out.println(d1.compareTo(d2) > 0);` | `TEST constructor y orden`<br>`Batería: 80.0%`<br>`true` |

```java
public abstract class Vehiculo {
    private String id;
    private String modelo;
    private double bateria;

    public Vehiculo(String id, String modelo, double bateria) {
        this.id = id;
        this.modelo = modelo;
        this.bateria = bateria;
    }

    public String getId() { return id; }
    public String getModelo() { return modelo; }
    public double getBateria() { return bateria; }
    public void setBateria(double bateria) { this.bateria = bateria; }

    public abstract String obtenerEstadoBateria();
}

// Declare la clase "Dron" para que cumpla la relación de herencia con
// "Vehiculo" y además implemente Comparable<Dron>

/* Complete aquí la declaración de la clase */ {

    private double capacidadCarga;

    public Dron(String id, String modelo, double bateria, double capacidadCarga) extends Vehiculo implements Comparable<Dron> {
        // TODO: completar llamada al constructor padre
        // TODO: asignar capacidadCarga
        super(id, modelo, bateria);
        this.capacidadCarga = capacidadCarga;
        
    }

    public double getCapacidadCarga() {
        // TODO: completar
        return this.capacidadCarga;
    }

    @Override
    public String obtenerEstadoBateria() {
        // TODO: devolver el texto "Batería: X%" usando getBateria()
        return "Batería: " + this.getBateria() + "%";
    }

    @Override
    public int compareTo(Dron otro) {
        // TODO: ordenar de menor a mayor batería
        return Double.compare(this.getBateria(), otro.getBateria());;
    }
}
```

---

### Pregunta 3 — Clase `EstacionCarga`

```
                EstacionCarga extends Vehiculo
                ---------------------------------------------
                -capacidadMaxima: int
                -dronesEnCarga: ArrayList<Dron>
                ---------------------------------------------
                +EstacionCarga(id: String, modelo: String, capacidadMaxima: int)
                +asignarDron(dron: Dron): void
                +recargarTodos(): void
                +obtenerEstadoBateria(): String
```

A diferencia de la `Ruta` (que solo *lee* la batería de sus drones), la `EstacionCarga` **modifica** el estado de los drones que tiene asignados: al recargar, debe llevar la batería de **todos** los drones que gestiona al 100%.

Nota: `EstacionCarga` hereda de `Vehiculo` pero **no usa** el atributo `bateria` heredado para representar su propia carga; ese atributo puede quedar en 100 fijo, y lo relevante acá es la lista de drones que administra.

**Por ejemplo:**

| Prueba | Resultado |
|---|---|
| `System.out.println("TEST recarga");`<br>`EstacionCarga estacion = new EstacionCarga("E1","Base Norte", 5);`<br>`Dron d1 = new Dron("D1","Delivery-X", 20.0, 2.5);`<br>`estacion.asignarDron(d1);`<br><br>`estacion.recargarTodos();`<br>`System.out.println(d1.getBateria());` | `TEST recarga`<br>`100.0` |

```java
public class EstacionCarga extends Vehiculo {

    private int capacidadMaxima;
    private ArrayList<Dron> dronesEnCarga;

    public EstacionCarga(String id, String modelo, int capacidadMaxima) {
        // TODO: completar llamada al constructor padre (bateria = 100)
        // TODO: asignar capacidadMaxima
        // TODO: inicializar dronesEnCarga
        super(id, modelo, 100);
        this.capacidadMaxima = capacidadMaxima;
        this.dronesEnCarga = new ArrayList<>();
    }

    /**
     * Asigna un dron a esta estación de carga.
     * Si ya se alcanzó la capacidadMaxima, debe lanzar FlotaException
     * con código 1 y el mensaje "Capacidad de estación excedida".
     */
    public void asignarDron(Dron dron) throws FlotaException {
        // TODO: si dronesEnCarga.size() ya alcanzó capacidadMaxima, lanzar FlotaException(1, "Capacidad de estación excedida")
        // TODO: agregar el dron a la lista
        if(dronesEnCarga.size() == this.capacidadMaxima) {
	        throw new FlotaException(1,  "Capacidad de estación excedida");
        } else { 
	        dronesEnCarga.add(dron);
        }
    }

    /**
     * Lleva la batería de todos los drones asignados al 100%.
     */
    public void recargarTodos() {
        // TODO: recorrer dronesEnCarga y setear bateria en 100 a cada uno
        for(Dron d : dronesEnCarga) {
		    d.setBateria(100);
        }
    }

    @Override
    public String obtenerEstadoBateria() {
        // TODO: devolver el texto "Estación operativa: N drones en carga"
        // donde N es la cantidad de drones asignados
        
        return "Escación operativa: "+ dronesEnCarga.size() + " drones en carga";
    }
}
```

---

### Pregunta 4 — Clase `Ruta` (agregación, mínimo y orden)

```
Ruta
--------------------------------------------------
-nombre: String
-drones: ArrayList<Dron>
-estacion: EstacionCarga
-estado: EstadoRuta
--------------------------------------------------
+Ruta(nombre: String, estacion: EstacionCarga)
+getNombre(): String
+getEstado(): EstadoRuta
+setEstado(estado: EstadoRuta): void
+obtenerBateriaMinima(): double
+ordenarDronesPorBateria(): void
+actualizarEstado(): void
```

A diferencia de un promedio, acá interesa el **peor caso**: la batería más baja entre todos los drones de la ruta, porque un solo dron sin batería puede frenar toda la entrega.

Complete los métodos indicados:

- inicializar el estado en `EstadoOperativa`
- implementar `getEstado()` / `setEstado(...)`
- implementar `obtenerBateriaMinima()`: recorre `drones` y devuelve el valor de batería **más bajo**. Si la lista está vacía, lanzar `FlotaException` con código `2` y mensaje `"La ruta no tiene drones asignados"`.
- implementar `ordenarDronesPorBateria()`: debe dejar la lista `drones` ordenada de menor a mayor batería usando `Collections.sort` (aprovechando que `Dron` implementa `Comparable`).
- completar `actualizarEstado()`:
  - batería mínima mayor a 40: `EstadoOperativa`
  - batería mínima entre 15 y 40 inclusive: `EstadoAlerta`
  - batería mínima menor a 15: `EstadoEmergencia`
  - luego, ejecutar el estado actual

**Por ejemplo:**

| Prueba | Resultado |
|---|---|
| `System.out.println("TEST bateria minima");`<br>`EstacionCarga estacion = new EstacionCarga("E1","Base Norte", 5);`<br>`RutaTest ruta = new RutaTest("Zona Centro", estacion);`<br>`ruta.agregarDron(new Dron("D1","X",80,2));`<br>`ruta.agregarDron(new Dron("D2","X",25,2));`<br><br>`System.out.println(ruta.getEstado().getNombre());`<br>`System.out.println(ruta.obtenerBateriaMinima());` | `TEST bateria minima`<br>`OPERATIVA`<br>`25.0` |

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.HashSet;

public class Ruta {

    private String nombre;
    private ArrayList<Dron> drones;
    private HashSet<Monitor> observadores;
    private EstacionCarga estacion;
    private EstadoRuta estado;

    public Ruta(String nombre, EstacionCarga estacion) {
        // TODO: inicializar el estado en EstadoOperativa
        // TODO: inicializar el resto de las variables de instancia
        // nombre, estacion, drones, observadores, etc.
        this.nombre = nombre;
        this.drones = new ArrayList<>();
        this.observadores = new HashSet<>();
        this.estacion = estacion;
        thiss.estado = new EstadoOperativa();
    }

    // NO TOCAR ESTOS METODOS, estos serán reemplazados para el testing
    // ASUMA QUE ESTAN CORRECTAMENTE IMPLEMENTADOS
    public String getNombre() { return nombre; }
    public ArrayList<Dron> getDrones() { return drones; }
    public void agregarDron(Dron dron) {}
    public HashSet<Monitor> getObservadores() { return observadores; }
    public void agregarObservador(Monitor m) {}
    public void notificarObservadores(String mensaje) {}
    public EstacionCarga getEstacion() { return estacion; }

    // Implementar a partir de aquí
    public EstadoRuta getEstado() {
        // TODO: devolver el estado actual
        return this.estado;
    }

    public void setEstado(EstadoRuta estado) {
        // TODO: modificar el estado actual
        this.estado = estado;
    }

    /**
     * Devuelve el valor de batería más bajo entre todos los drones
     * de la ruta.
     * @throws FlotaException codigo 2 si la ruta no tiene drones
     */
    public double obtenerBateriaMinima() throws FlotaException {
        // TODO: si drones está vacío, lanzar new FlotaException(2, "La ruta no tiene drones asignados")
        // TODO: recorrer drones y devolver el valor mínimo de batería
        if(drones.isEmpty()) {
	        throw new FlotaException(2, "La ruta no tiene drones asignados");
        } else {
	        Dron chico = drones.get(0);
	        for(Dron d, drones) {
		        if(d.getBateria() < chico.getBateria()) { 
			        chico = d;
		        }
	        }
	        return chico.getBateria();
        }
    }

    /**
     * Ordena la lista de drones de menor a mayor batería.
     */
    public void ordenarDronesPorBateria() {
        // TODO: usar Collections.sort sobre "drones"
        Collections.sort(drones);
        
    }

    public void actualizarEstado() throws FlotaException {
        // TODO: obtener la bateria minima (usar obtenerBateriaMinima)
        // TODO: asignar el estado que corresponda según el valor
        // TODO: ejecutar el estado actual
        //- batería mínima mayor a 40: `EstadoOperativa`
		//- batería mínima entre 15 y 40 inclusive: `EstadoAlerta`
		//- batería mínima menor a 15: `EstadoEmergencia`
		//- luego, ejecutar el estado actual
		double bat = this.obtenerBateriaMinima();
        if(bat > 40) { 
	        this.setEstado(new EstadoOperativa());
        } else if (bat >= 15 && bat <=40) {
	        this.setEstado(new EstadoAlerta());
        } else if (bat < 15) {
	        this.setEstado(new EstadoEmergencia());
        }
        this.estado.ejecutar(this);
    }
}
```

---

### Pregunta 5 — Clase `ControladorFlota`

```
ControladorFlota
--------------------------------------------------
-rutas: HashMap<String, Ruta>
--------------------------------------------------
+ControladorFlota()
+agregarRuta(ruta: Ruta): void
+buscarRuta(nombre: String): Ruta
+ejecutarCicloControl(): void
+listarRutasEnEmergencia(): ArrayList<String>
```

A diferencia de simplemente ejecutar una acción sobre una ruta puntual, acá se pide además un método de **consulta/filtrado** sobre todas las rutas administradas.

Complete:

- `agregarRuta(...)`
- `buscarRuta(...)`: si no existe la ruta, lanzar `FlotaException` con código `3` y mensaje `"No existe una ruta con ese nombre"`.
- `ejecutarCicloControl()`: recorre todas las rutas y ejecuta `actualizarEstado()` sobre cada una.
- `listarRutasEnEmergencia()`: recorre todas las rutas y devuelve una lista con los **nombres** de aquellas cuyo estado actual sea `EstadoZona.EMERGENCIA` (usar `getEstado().getNombre()` para comparar contra el enum).

**Por ejemplo:**

| Prueba | Resultado |
|---|---|
| `System.out.println("TEST listar en emergencia");`<br>`ControladorFlota controlador = new ControladorFlota();`<br>`// ... se agregan 3 rutas, una de ellas queda en EMERGENCIA tras ejecutarCicloControl()`<br>`controlador.ejecutarCicloControl();`<br>`System.out.println(controlador.listarRutasEnEmergencia());` | `TEST listar en emergencia`<br>`[Zona Sur]` |

```java
public class ControladorFlota {

    // La clase posee un HashMap<String, Ruta>, donde la clave es el
    // nombre de la ruta.
    private HashMap<String, Ruta> rutas;

    public ControladorFlota() {
        // TODO: inicializar el mapa de rutas
        this.rutas = new HashMap<>();
    }

    public void agregarRuta(Ruta ruta) {
        // TODO: agregar la ruta al mapa usando su nombre como clave
        rutas.put(ruta.getNombre(), ruta);
    }

    /**
     * Busca una Ruta por nombre.
     * @throws FlotaException codigo 3 si no existe una ruta con ese nombre.
     */
    public Ruta buscarRuta(String nombre) throws FlotaException {
        // TODO: si no existe, lanzar new FlotaException(3, "No existe una ruta con ese nombre")
        // TODO: devolver la ruta correspondiente
	    if (rutas.containsKey(nombre)) {
	        return rutas.get(nombre);
	    } else {
	        throw new FlotaException(3, "No existe una ruta con ese nombre");
    }
}

    public void ejecutarCicloControl() throws FlotaException {
        // TODO: recorrer todas las rutas del mapa
        // TODO: ejecutar actualizarEstado() sobre cada una
        for(Ruta r : rutas.values()) {
	        r.actualizarEstado();
        }
    }
    
    /**
     * Devuelve los nombres de todas las rutas cuyo estado actual
     * es EMERGENCIA.
     */
    public ArrayList<String> listarRutasEnEmergencia() {
        // TODO: recorrer las rutas del mapa
        // TODO: si el estado de la ruta es EstadoZona.EMERGENCIA, agregar su nombre a la lista de resultado
        ArrayList<String> ru = new ArrayList<>();
        for(Ruta r : rutas.values()) { 
	        if(r.getEstado().getNombre() == Estadozona.EMERGENCIA) { 
		        ru.add(r.getNombre());
	        }
        }
        return ru;
    }
}
```

---

### Pregunta 6 — Clase `EstadoAlerta` y excepción `FlotaException`

Considere nuevamente el diagrama de la Pregunta 4, y la interfaz `EstadoRuta`:

```
<<interface>> EstadoRuta
--------------------------------
+ejecutar(ruta: Ruta): void
+getNombre(): EstadoZona
```

Además, se pide declarar la excepción `FlotaException`, que **a diferencia de una excepción simple**, debe guardar un código numérico además del mensaje.

**Parte A — `FlotaException`**

```java
// Declare la clase "FlotaException" de forma tal que:
// - extienda de Exception
// - tenga un constructor que reciba (int codigo, String mensaje)
// - guarde el código en un atributo privado
// - exponga un método getCodigo(): int
// - al llamar a getMessage() (heredado de Exception) devuelva el mensaje recibido

/* Complete aquí la declaración de la clase */ 
public class FlotaException extends Exception {
    private int codigo;

    public FlotaException(int codigo, String mensaje){
        // TODO: invocar al constructor de Exception pasando el mensaje
        // TODO: asignar el código
        super(mensaje);
        this.codigo = codigo;
    }

    public int getCodigo() {
        // TODO: completar
        return this.codigo;
    }
}
```

**Parte B — `EstadoAlerta`**

Cuando una ruta entra en estado de alerta (batería mínima entre 15 y 40), el sistema debe:

1. Ordenar los drones de la ruta por batería (usar `ordenarDronesPorBateria()`).
2. Notificar a los observadores de la ruta el mensaje: `"La ruta está en ALERTA. Se recomienda enviar el dron con menor batería a recargar."`
3. El nombre a retornar en `getNombre()` es el valor correspondiente del enum `EstadoZona`.

**Por ejemplo:**

| Prueba | Resultado |
|---|---|
| `System.out.println("TEST constructor");`<br>`EstadoAlerta estado = new EstadoAlerta();`<br><br>`System.out.println("EstadoAlerta es un EstadoRuta: " + (estado instanceof EstadoRuta));`<br>`System.out.println("Estado: " + estado.getNombre());` | `TEST constructor`<br>`EstadoAlerta es un EstadoRuta: true`<br>`Estado: ALERTA` |

```java
// Codifique la clase EstadoAlerta tal que implemente la interfaz EstadoRuta
//
// Al ejecutarse:
//  1) debe ordenar los drones de la ruta por batería
//  2) debe notificar a los observadores el mensaje indicado arriba
//  3) getNombre() debe devolver EstadoZona.ALERTA
public class EstadoAlerta implements EstadoRuta { 
	@Override
	public void Ejecutar(Ruta ruta) {
		ruta.ordenarDronesPorBateria();
		ruta.notificarObservadores("La ruta está en ALERTA. Se recomienda enviar el dron con menor batería a recargar.");
	}
	@Override
	public EstadoRuta getNombre() { 
		return EstadoZona.ALERTA;
	}
}

```

---

## Notas para resolver el práctico

- Este parcial evalúa los **mismos temas** que el original (herencia con clase abstracta, interfaces, patrón *State*, patrón *Observer*, colecciones, excepciones *checked* propias), pero con un diseño de clases distinto:
  - Acá hay **dos** patrones adicionales entrelazados: `Comparable` para poder ordenar (Pregunta 2 y 4) y una excepción que **guarda un dato extra** además del mensaje (Pregunta 6, Parte A).
  - En vez de un promedio, el cálculo relevante es un **mínimo** (peor caso).
  - En vez de solo ejecutar una acción puntual sobre un elemento del mapa, el `ControladorFlota` pide además un método de **filtrado/consulta** (`listarRutasEnEmergencia`) que recorre todos los valores del `HashMap`.
  - `EstacionCarga` no es un simple dispositivo con `abrir()/cerrar()`: administra una colección propia de drones y **modifica el estado de otros objetos** (les setea la batería), algo que no aparecía en el original.
- Te conviene escribir también las clases `EstadoOperativa` y `EstadoEmergencia` (no pedidas explícitamente) para poder probar `actualizarEstado()` de punta a punta antes de dar por terminado el ejercicio.
