Respuestas del [[Final]]

![[{91C1C7A2-1E10-4F32-B0B0-07581A282A24}.png]]

```
public class ZonaRiego {

    private String nombre;
    private ArrayList<SensorHumedad> sensores;

    public ZonaRiego(String nombre) {
        // TODO: asignar el nombre
        // TODO: inicializar la lista de sensores
        this.nombre = nombre;
        sensores = new ArrayList<>();
    }

    public String getNombre() {
        // TODO: completar
        return nombre;
    }

    /** 
     * Agrega un sensor a la zona de Riego
     */
    public void agregarSensor(SensorHumedad sensor) {
        // TODO: agregar el sensor a la lista
        sensores.add(sensor);
        
    }

    public int getCantidadSensores(){
        // TODO: implementar
        return sensores.size();
    }
    
    /**
     * Calcula el promedio de humedad de todos los sensores
     * de la Zona.
     * @throws RiesgoException si no hay sensores
     */
    public double calcularHumedadPromedio() throws RiegoException {
        // TODO: si no hay sensores, lanzar RiegoException
        if(sensores.isEmpty()) {
            throw new RiegoException("");
        } else {
            
            double cantidad= 0.0;
            for (SensorHumedad s : sensores) {
                cantidad = cantidad + s.getHumedad();
            }
            double promedio = cantidad / sensores.size();
        
        return promedio;
        }
    }
}
```
![[{1B39BB23-3769-4814-BF4F-5F44CBF3DB84}.png]]

```
// Declare la clase "ValvulaRiego" para que cumpla la relación de herencia con 
// la clase "Dispositivo"
public class ValvulaRiego extends Dispositivo {

/* Complete aquí la declaracion de la clase*/  

    private boolean abierta;

    public ValvulaRiego(String id, String nombre) {
        // TODO: completar llamada al constructor padre
        // TODO: inicializar la válvula cerrada
        super(id, nombre);
        this.abierta = false;
    }

    public void abrir() throws RiegoException {
        // TODO: si la válvula está inactiva, lanzar RiegoException
        // TODO: abrir la válvula
        if(!this.isActivo()) { 
            throw new RiegoException("");
        } else {
            abierta = true;
        }
    }

    public void cerrar() {
        // TODO: cerrar la válvula
        abierta = false;
    }

    public boolean isAbierta() {
        // TODO: completar
        if(abierta == true) {
            return true;
        } else {
        return false;
        }
    }

    @Override
    public String obtenerDescripcionEstado() {
        // TODO: completar
        // Retorna el texto "Valvula abierta" o "Valvula cerrada" segun corresponda
        if(abierta == true) { 
            return "Valvula abierta";
        } else {
            return "Valvula cerrada";
        }
    }
}
```
![[{B6CAA591-FDA1-4686-B820-0A0D80B2607F}.png]]

``` java
//import java.util.ArrayList;
//import java.util.HashSet;

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
        this.estado = new EstadoNormal(); 
        this.nombre = nombre; 
        this.valvula  = valvula;
        sensores = new ArrayList<>();
        observadores= new HashSet<>();
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
        
        return this.valvula;
    }

    public EstadoRiego getEstado() {
        // TODO: devolver el estado actual
        return this.estado;
    }

    public void setEstado(EstadoRiego estado) {
        // TODO: modificar el estado actual
		this.estado = estado;
    }

    public void actualizarEstado() throws RiegoException {
        // TODO: calcular la humedad promedio (utilice el método calcularHumedad)
        // TODO: si el promedio es mayor a 50, asignar EstadoNormal
        // TODO: si el promedio está entre 20 y 50 inclusive, asignar EstadoSeco
        // TODO: si el promedio es menor a 20, asignar EstadoRegando
        // TODO: ejecutar el estado actual
        double s = sensores.cacluclarHumedadPromedio();
        if(s > 50) {
           this.setEstado(new EstadoNormal()) ;
        } else if (s >= 20 && s <= 50) {
            this.setEstado(new EstadoSeco());
        } else if (s < 20 ) {
            this.setEstado(new EstadoRegando());
        }
        this.estado.ejecutar(this)
    }

    public void regar() throws RiegoException {
        // TODO: asignar EstadoRegando
        // TODO: ejecutar el estado actual
        this.setEstado(new EstadoRegando());
        this.estado.ejecutar(this);
        
    }
}
```

![[{9DCD2DE9-FB1F-4576-BFC3-4D7C35DD2395}.png]]
```java
public class ControladorRiego {

    //La clase posee un HashMap<String, ZonaRiego>, donde la clave es el nombre de la zona.
    private HashMap<String, ZonaRiego> zonas;

    public ControladorRiego() {
        // TODO: inicializar el mapa de zonas
        this.zonas = new HashMap<>();
    }

    public void agregarZona(ZonaRiego zona) {
        // TODO: agregar la zona al mapa usando su nombre como clave
        zonas.put(zona.getNombre(), zona);
    }

    /** 
     * Busca una ZonaReigo por nombre
     * lanzar una RiegoException si no existe una zona con el nombre recibido.
     */
    public ZonaRiego buscarZona(String nombre) throws RiegoException {
        // TODO: si no existe la zona, lanzar RiegoException
        // TODO: devolver la zona correspondiente
        if(nombre != null)  {
            if(zonas.containsKey(nombre)) {
                return zonas.get(nombre);
            } else { 
                throw new RiegoException("");
            }
        } 
        throw new RiegoException("");
    }

    public void regarZona(String nombre) throws RiegoException {
        // TODO: buscar la zona por nombre
        // TODO: ejecutar el método regar() de la zona
        if(zonas.containsKey(nombre))  {
            zonas.get(nombre).regar();
        }
    }

    /**
     * El metodo ejecutarCicloControl representa un “tick” del reloj del
     * sistema: debe recorrer todas las zonas y actualizar 
     * el estado de cada una.
     */
    public void ejecutarCicloControl() throws RiegoException {
        // TODO: recorrer todas las zonas del mapa
        // TODO: ejecutar actualizarEstado() sobre cada zona
        for(ZonaRiego z : zonas.values() ) {
            z.actualizarEstado();
        }
            
    }
}

```

![[{A158578D-B19C-4F27-9777-41AE73E22B32}.png]]


```java
// Codifique la clase EstadoSeco tal que implemente la interfaz EstadoRiego
public class EstadoSeco implements EstadoRiego { 
// Cuando se ejecuta este estado, debe cerrar la valvula ede la zona de riego
// y notificar a los observadores de la zona un mensaje:
// "La zona está SECA. Todavía no se inicia el riego."
// El nombre a retonrar es el valor correspondiente del enum EstadoZona.
	@Override
    public void Ejecutar(ZonaRiego zona) { 
        zona.getValvula().cerrar();
        notificarObservadores("Lazona está SECA. Todavia no se inicia el riego");
    }
    @Override
    public EstadoZona getNombre() {
        return EstadoZona.SECA;
    }
}
```



