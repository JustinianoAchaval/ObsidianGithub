![[{CD4B2DE4-B7DC-48BD-9A73-1160077AEA93}.png]]


![[{8520F2CF-B894-421C-AB49-A4B57E8B139F}.png]]

```java
public class ZonaRiego {

    private String nombre;
    private ArrayList<SensorHumedad> sensores;

    public ZonaRiego(String nombre) {
        // TODO: asignar el nombre
        // TODO: inicializar la lista de sensores
        this.nombre = nombre; 
        this.sensores = new ArrayList<>();
    }

    public String getNombre() {
        // TODO: completar
        return this.nombre;
    }

    /** 
     * Agrega un sensor a la zona de Riego
     */
    public void agregarSensor(SensorHumedad sensor) {
        // TODO: agregar el sensor a la lista
        this.sensores.add(sensor);
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
	    if (sensores.isEmpty()) {
		    throw new RiegoException("");
	    } else {
	        double calPromedio = 0.0;
		    for(Sensores s : sensores) {
		        calPromedio += s.getHumedad();
	        }
	    return calPromedio/sensores.size();
        }
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
        super(id, nombre);
        this.abierta = false;
    }

    public void abrir() throws RiegoException {
        // TODO: si la válvula está inactiva, lanzar RiegoException
        // TODO: abrir la válvula
        if(!this.isActivo()) { 
	        throw new RiegException("");
        } else { 
	        this.abierta = true;
        }
    }

    public void cerrar() {
        // TODO: cerrar la válvula
        this.abierta = false; 
    }

    public boolean isAbierta() {
        // TODO: completar
        if(this.abierta == true) { 
	        return true;
        } else {
	        return false;
	    }
    }

    @Override
    public String obtenerDescripcionEstado() {
        // TODO: completar
        // Retorna el texto "Valvula abierta" o "Valvula cerrada" segun corresponda
        if(this.abierta == true) { 
	        String mensaje = "Valvula Abierta";
	        return mensaje;
        } else {
	        String mensaje = "Valvula Cerrada";
	        return mensaje;
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
        this.nombre = nombre; 
        this.sensores = new ArrayList<>();
        this.observadores = new HashMap<>();
        this.valvula = valvula;
        this.estado = new EstadoNormal();
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
        double promedio = this.calcularHumedadPromedio();
        // TODO: si el promedio es mayor a 50, asignar EstadoNormal
        // TODO: si el promedio está entre 20 y 50 inclusive, asignar EstadoSeco
        // TODO: si el promedio es menor a 20, asignar EstadoRegando
        // TODO: ejecutar el estado actual
        if(promedio > 50) {
	        this.setEstado(new EstadoNormal());
        } else if (promedio <= 50 && promedio >= 20) {
	        this.setEstado(new EstadoSeco());
        } else if (promedio < 20) {
	        this.setEstado(new EstadoRegando());
        }
        this.estado.ejecutar(this);
    }

    public void regar() throws RiegoException {
        // TODO: asignar EstadoRegando
        // TODO: ejecutar el estado actual
        this.setEstado(new EstadoRegando());
        this.estado.ejecutar(this);
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
        if(zonas.containsKey(nombre)) { 
	        zonas.get(nombre).regar();
        } else { 
	        throw new RiegoException("");
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
	    for(ZonaRiego z : zonas.values()) { 
		    z.actualizarEstado();
        }
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

public class EstadoSeco implements EstadoRiego{ 
	@Override
	public void ejecutar(ZonaRiego zona) {
		zona.getValvula().cerrar();
		zona.notificarObservadores("La zona está SECA. Todavía no se inicia el riego.");
	}
	@Override
	public EstadoZona getNombre() { 
		return EstadoZona.SECA;
	}
}

```

PRACTICAR LA DEFINICION DE CLASES Y MAS SOBRE LOS ENUM
