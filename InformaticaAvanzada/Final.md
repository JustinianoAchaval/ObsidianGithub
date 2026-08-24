![[{CD4B2DE4-B7DC-48BD-9A73-1160077AEA93}.png]]


![[{8520F2CF-B894-421C-AB49-A4B57E8B139F}.png]]

```java
public class ZonaRiego {

    private String nombre;
    private ArrayList<SensorHumedad> sensores;

    public ZonaRiego(String nombre) {
        // TODO: asignar el nombre
        // TODO: inicializar la lista de sensores
    }

    public String getNombre() {
        // TODO: completar
        return null;
    }

    /** 
     * Agrega un sensor a la zona de Riego
     */
    public void agregarSensor(SensorHumedad sensor) {
        // TODO: agregar el sensor a la lista
    }

    public int getCantidadSensores(){
        // TODO: implementar
    }
    
    /**
     * Calcula el promedio de humedad de todos los sensores
     * de la Zona.
     * @throws RiesgoException si no hay sensores
     */
    public double calcularHumedadPromedio() throws RiegoException {
        // TODO: si no hay sensores, lanzar RiegoException

        return 0;
    }
}
```

![[Pasted image 20260719232257.png]]

```Java
// Declare la clase "ValvulaRiego" para que cumpla la relación de herencia con 
// la clase "Dispositivo"

/* Complete aquí la declaracion de la clase*/  {

    private boolean abierta;

    public ValvulaRiego(String id, String nombre) {
        // TODO: completar llamada al constructor padre
        // TODO: inicializar la válvula cerrada
    }

    public void abrir() throws RiegoException {
        // TODO: si la válvula está inactiva, lanzar RiegoException
        // TODO: abrir la válvula
    }

    public void cerrar() {
        // TODO: cerrar la válvula
    }

    public boolean isAbierta() {
        // TODO: completar
        return false;
    }

    @Override
    public String obtenerDescripcionEstado() {
        // TODO: completar
        // Retorna el texto "Valvula abierta" o "Valvula cerrada" segun corresponda
        return null;
    }
}
```

![[Pasted image 20260719231841.png]]

```Java
import java.util.ArrayList;
import java.util.HashSet;

public class ZonaRiego {

    private String nombre;
    private ArrayList<SensorHumedad> sensores;
    private HashSet<Visualizador> observadores;
    private ValvulaRiego valvula;
    private EstadoRiego estado;

    public ZonaRiego(String nombre, ValvulaRiego valvula) {
        // TODO: inicializar el estado en EstadoNormal
        // TODO: Inicializar el resto de las variables de instancia 
        // nombre, valvula, sensores, etc.
     }

//NO TOCAR ESTOS METODOS, estos serán reemplazados para el testing
//ASUMA QUE ESTAN CORRECTAMENTE IMPLEMENTADOS
    public String getNombre() {return nombre;}
    public HashSet<Visualizador> getObservadores(){ return observadores;}
    public ArrayList<SensorHumedad> getSensores(){ return sensores;}
    public double calcularHumedadPromedio() throws RiegoException{return 0.0;}
    public void agregarObservador(Visualizador observador) {}
    public void quitarObservador(Visualizador observador) {}
    public void notificarObservadores(String mensaje) {}

//Implementar a partir de aquí
    public ValvulaRiego getValvula() {
        // TODO: devolver la válvula
        return null;
    }

    public EstadoRiego getEstado() {
        // TODO: devolver el estado actual
        return null;
    }

    public void setEstado(EstadoRiego estado) {
        // TODO: modificar el estado actual
    }

    public void actualizarEstado() throws RiegoException {
        // TODO: calcular la humedad promedio (utilice el método calcularHumedad)
        // TODO: si el promedio es mayor a 50, asignar EstadoNormal
        // TODO: si el promedio está entre 20 y 50 inclusive, asignar EstadoSeco
        // TODO: si el promedio es menor a 20, asignar EstadoRegando
        // TODO: ejecutar el estado actual
    }

    public void regar() throws RiegoException {
        // TODO: asignar EstadoRegando
        // TODO: ejecutar el estado actual
    }
}
```

![[Pasted image 20260719231858.png]]

```Java
public class ControladorRiego {

    //La clase posee un HashMap<String, ZonaRiego>, donde la clave es el nombre de la zona.
    private HashMap<String, ZonaRiego> zonas;

    public ControladorRiego() {
        // TODO: inicializar el mapa de zonas
    }

    public void agregarZona(ZonaRiego zona) {
        // TODO: agregar la zona al mapa usando su nombre como clave
    }

    /** 
     * Busca una ZonaReigo por nombre
     * lanzar una RiegoException si no existe una zona con el nombre recibido.
     */
    public ZonaRiego buscarZona(String nombre) throws RiegoException {
        // TODO: si no existe la zona, lanzar RiegoException
        // TODO: devolver la zona correspondiente
        return null;
    }

    public void regarZona(String nombre) throws RiegoException {
        // TODO: buscar la zona por nombre
        // TODO: ejecutar el método regar() de la zona
    }

    /**
     * El metodo ejecutarCicloControl representa un “tick” del reloj del
     * sistema: debe recorrer todas las zonas y actualizar 
     * el estado de cada una.
     */
    public void ejecutarCicloControl() throws RiegoException {
        // TODO: recorrer todas las zonas del mapa
        // TODO: ejecutar actualizarEstado() sobre cada zona
    }
}
```

![[Pasted image 20260719231911.png]]

```Java
// Codifique la clase EstadoSeco tal que implemente la interfaz EstadoRiego

// Cuando se ejecuta este estado, debe cerrar la valvula ede la zona de riego
// y notificar a los observadores de la zona un mensaje:
// "La zona está SECA. Todavía no se inicia el riego."
// El nombre a retonrar es el valor correspondiente del enum EstadoZona.

```
