![[{16B7F6BE-FE08-490C-96E4-509025286AD4}.png]]

```java
public class Rectangulo {
    public int base;
    /**
     * si el argumento base es valido, setea el valor y retorna true
     * Si el valor es invalido, ignora el valor y retorna false
     * @param base. La base valida debe ser un numero entre 0 y 500
     */
    public boolean setBase(int base){
       //TODO: Implemente el metodo
        //No olvide eliminar la siguiente linea antes de implementar el metodo
          throw new RuntimeException();
    }
    /**
     * Retorna el valor de base
     */
    public int getBase (){
       //TODO: Implemente el metodo
        //No olvide eliminar la siguiente linea antes de implementar el metodo
        throw new RuntimeException();
    }
}
```

![[{862D40BF-102F-4A0E-8BFE-732A81ABA7AF}.png]]

```java
public class Evaluacion {

	/**
	 * Retorna una lista con los elementos de la
	 * lista pasada como argumento que comienzan
	 * con el prefijo especificado (no consideramos
	 * espacios iniciales ni mayusculas/minusculas)
	 */
	public ArrayList<String> FiltrarPorPrefijo (String prefijo, ArrayList<String> lista) {
	    //Implementar metodo
	    return null;
	}
}
```

![[{0A317636-2B0E-49DF-8EF2-65C6576AE201}.png]]

Resultado: 

![[{7F44B27A-7BE9-4552-8F4F-472A889E7991}.png]]

```java
import java.util.HashMap;

public class Carta {
    HashMap <Bebida,Integer> carta;
    
    /**
     *  Inicializa un HashMap para almacenar todas las bebidas del enumerado
     *  y sus precios. Debe asignar precio por defecto 30
     **/
    public Carta (){
        //TODO Implementar 
    }
    /**
     *  Ajusta el precio de una bebida en particular
     **/
    public void setPrecio (Bebida b, int precio){
        carta.put(b,precio);
    }
    /**
     *  Retorna el precio de una bebida en particular
     **/
    public int getPrecio(Bebida b){
        return carta.get(b);
    }

    /**
     *  Retorna el HashMap Carta
     **/
    public HashMap<Bebida,Integer> getCarta(){
        return carta;
    }

}
```

![[{C3E0AE04-AFEB-4AA0-BBEE-C200BF001285}.png]]

```java
//Modifique la definicion de la clase para realizar la herencia 
public class Escudo {
	//Defina los atributos necesarios de la clase
	//Implemente los siguientes metodos
    /**
     * Constructor de la clase Escudo.
     * El nombre es el nombre de la clase.
     */
    public Escudo (Integer ataque) {
	    //TODO Implementar constructor
    }

    public String getNombre() {
		//TODO Implementar metodo
    }
}
```

![[{584DF7B4-36C5-4325-89B4-308C8E7B5DCE}.png]]

```java
public class Transportes {
    ArrayList<???> moviles;

    public Transportes () {
        moviles = new ArrayList<>();
    }

    public void addMovil (???) {
        // TODO implementar
    }

    public ArrayList<???> getAereos () {
        // TODO implementar
        return null;
    }
}
```

![[{BD808C40-AA11-49E3-9E0B-C115CB51F499}.png]]

```java
public class Triciclo extends Vehiculo {
    // Completar con los metodos indicados
    // en el UML de la consigna
}
```
