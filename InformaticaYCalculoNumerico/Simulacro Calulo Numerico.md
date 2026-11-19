### Ejercicio 1: Enfriamiento de una pieza metálica

Se estudia el enfriamiento de una barra de acero mediante mediciones discretas de temperatura en distintos instantes de tiempo. El flujo de calor por conducción en la superficie viene dado por la ley de Fourier $q = -k \frac{dT}{dt}$, donde $k$ es la conductividad térmica.

Los datos registrados en el laboratorio son los siguientes:

|**Tiempo t (s)**|**Temperatura T (°C)**|
|---|---|
|0|180.0|
|5|145.2|
|10|118.4|
|15|98.1|
|20|82.5|

Se desea estimar **qué tan rápido cambia la temperatura** ($\frac{dT}{dt}$) exactamente en el instante $t = 10\text{ s}$ aprovechando que las mediciones están igualmente espaciadas ($\Delta t = 5\text{ s}$).

1. **¿A qué tipo de problema de cálculo numérico corresponde?** Diferenciacion Numerica
    
2. **Elija el método o los métodos que sean aplicables a la resolución de este problema:** Métodos de Interpolación de Newton y Lagrange.
    
3. **¿Tipo de error que predomina en el/los método/s de resolución para este problema?**
    Errores de Truncamiento
4. **En base al error que predomina, ¿Qué sugiere realizar para minimizar el error en este problema particular?**
    Utilizar Mediciones Adyacentes

### Ejercicio 2: Caudal en un canal de riego

Para evaluar el abastecimiento hídrico de una parcela, se midió el caudal de agua $Q$ ($\text{m}^3/\text{s}$) que ingresa por una compuerta a lo largo de una jornada de 12 horas. El volumen total de agua acumulado en el reservorio se expresa como $V = \int_{0}^{12} Q(t)\,dt$.

|**Tiempo t (h)**|**Caudal Q (m3/s)**|
|---|---|
|0|1.2|
|2|1.8|
|5|2.5|
|9|2.1|
|12|1.4|

Se desea determinar el **volumen total de agua acumulado** en el reservorio al cabo de las 12 horas utilizando los datos tabulados (note que los intervalos de tiempo no son uniformes).

1. **¿A qué tipo de problema de cálculo numérico corresponde?**
    Integracion Numerica 
2. **Elija el método o los métodos que sean aplicables a la resolución de este problema:**
    Metodo de Trapecio compuesto
3. **¿Tipo de error que predomina en el/los método/s de resolución para este problema?**
    Errores de truncamiento 
4. **En base al error que predomina, ¿Qué sugiere realizar para minimizar el error en este problema particular?**
     USar todas las mediciones

### Ejercicio 3: Perfil de densidad en una columna atmosférica

En meteorología, la densidad del aire $\rho$ ($\text{kg/m}^3$) disminuye con la altitud $z$ ($\text{km}$), afectando la sustentación de aeronaves. A partir de una sonda meteorológica se obtuvieron los siguientes registros:

|**Altitud z (km)**|**Densidad ρ (kg/m3)**|
|---|---|
|0|1.225|
|2|1.007|
|4|0.819|
|6|0.660|
|8|0.526|

Se desea estimar el valor de la densidad del aire $\rho$ a una **altitud intermedia** de $z = 3.2\text{ km}$ construyendo un polinomio de segundo grado.

1. **¿A qué tipo de problema de cálculo numérico corresponde?**
    Interpolacion
2. **Elija el método o los métodos que sean aplicables a la resolución de este problema:**
    Lagranje
3. **¿Tipo de error que predomina en el/los método/s de resolución para este problema?**
    Error de truncamiento
4. **En base al error que predomina, ¿Qué sugiere realizar para minimizar el error en este problema particular?**
    Utilizo mediciones adyacentes

### Ejercicio 4: Balance de masas en reactores conectados

Tres reactores químicos están interconectados mediante tuberías que transportan una solución salina en estado estacionario. Planteando la conservación de masa en cada tanque se obtiene el siguiente sistema de ecuaciones que vincula las concentraciones $c_1, c_2$ y $c_3$:

$$\begin{cases} 6c_1 - 2c_2 - c_3 = 120 \\ -3c_1 + 8c_2 - 2c_3 = 85 \\ -c_1 - 2c_2 + 5c_3 = 50 \end{cases}$$

Se desea calcular simultáneamente las concentraciones de equilibrio $c_1, c_2$ y $c_3$ en cada reactor.

1. **¿A qué tipo de problema de cálculo numérico corresponde?**
    Sistemas lineales 
2. **Elija el método o los métodos que sean aplicables a la resolución de este problema:**
    Gauss
3. **¿Tipo de error que predomina en el/los método/s de resolución para este problema?**
    Redondeo
4. **En base al error que predomina, ¿Qué sugiere realizar para minimizar el error en este problema particular?**
	Usar precicion doble