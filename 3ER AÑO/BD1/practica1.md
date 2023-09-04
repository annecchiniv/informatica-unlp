**1) Cuadros**

![cuadro-ej1](https://github.com/annecchiniv/informatica-unlp/blob/master/3ER%20A%C3%91O/BD1/CUADROS/cuadro1-ej1.jpg?raw=true)

    Hay 2 relaciones con el mismo nombre “expuesto" y esto es un error ya que 
    no pueden haber dos relaciones/entidades con el mismo nombre 
    por lo tanto habría que modificar el nombre de alguna.
    Entonces corrijo el error y cambio a "expone" el nombre de la relación "expuesto" 
    entre la agregación y la entidad periodo
    
![cuadro1.2-ej1](https://github.com/annecchiniv/informatica-unlp/blob/master/3ER%20A%C3%91O/BD1/CUADROS/cuadro1.2-ej1.jpg?raw=true)

A. En este modelo cada período de exposición contiene múltiples cuadros en museos. ¿Qué
parte del modelo indica esto? ¿Cómo la modificaría para que cada período fuese exclusivo de
cada cuadro expuesto en un museo?

    ¿Qué parte del modelo indica esto?
    La parte del modelo que indica que cada período de exposición 
    contiene múltiples cuadros en museos es la cardinalidad (1,N) 
    de la relación Expone del lado de la agregación.  
    
![cuadro1.3-ej1](https://github.com/annecchiniv/informatica-unlp/blob/master/3ER%20A%C3%91O/BD1/CUADROS/cuadro1.3-ej1.jpg?raw=true)
    
    ¿Cómo la modificaría para que cada período fuese exclusivo de cada cuadro expuesto en un museo?
    Modificaria la cardinalidad antes mencionada a (1,1) 
    

B. Si los cuadros se expusieran en un solo período dentro de cada museo ¿cómo ajustaría el modelo para reflejar esto?

    Cambiaria la otra cardinalidad (del lado de Periodo) a (1,1) 

C. Ajuste el modelo para representar museos de dos tipos: de **arte contemporáneo**, con fecha de inauguración, país y director;  y de **arte en general**, del cual se conoce una fecha estimada de inauguración, país, director y datos históricos. De los datos históricos se registra un año y una descripción histórica, por ejemplo que una pintura famosa se exhibió por primera vez allí en un año determinado.

**2) Verdadero o falso. Justificar**

A. En una especialización, la entidad padre no modela datos que realmente existan, sino
que sirve para representar los aspectos comunes de las entidades hijas.

    Falso. La entidad padre SI modela datos que existen y también sirve para
    representar aspectos comunes de entidades hijas.

B. En una agregación, la cardinalidad mínima debe ser mayor a cero

    Falso. En una agregación la cardinalidad mínima da igual. 
    Lo que importa es la cardinalidad máxima que debe ser siempre mayor que 1.

C. Una entidad puede no tener un atributo identificador en el modelo ER

    Falso. Siempre tiene que tener un atributo identificador. 

D. No es correcto modelar atributos en las relaciones en un modelo ER

    Falso. Se puede mientras no sea un atributo identificador. 

**3) Verdadero/ Falso. Justificar**

![cuadro-ej3](https://github.com/annecchiniv/informatica-unlp/blob/master/3ER%20A%C3%91O/BD1/CUADROS/cuadro-ej3.jpg?raw=true)

A. La relación tiene está mal definida, ya que debería ser entre persona y categoría_monotributo.

    Falso. Está bien definida porque el enunciado dice que solo de las personas físicas
    se conoce categoría de monotributo.

B. La relación realiza esta bien definida, ya que todas las personas realizan actividades.

    Verdadero. El enunciado dice que de cada beneficiario se conoce la actividad económica. 

C. La jerarquía de Persona representa correctamente la problemática.

    Falso.
    - La entidad Persona podría llamarse Beneficiario para que el modelo sea más claro.
    - Esta entidad podría ser Generalización porque no hay otro tipo de persona para este enunciado.
    - Además tiene que modelar datos comunes de entidades hijas (dpto, provincia, localidaad) y no lo hace. 

D. La relación pertenece está mal definida, ya que no puede haber atributos en las relaciones.

    Falso. Puede haber atributos en las relaciones, mientras no sean identificador.

E. La agregación de la relación posee está correctamente definida ya que con una relación uno a muchos se puede agregar.

    Falso. Esta mal definida porque se puede agregar si ambas cardinalidades maximas son mayor que 1. 

F. Con este diseño es posible conocer el saldo disponible del subsidio para futuras liquidaciones.

    Verdadero. Se podría conocer calculandolo con sumas por mes total_gastado y se resta al monto del Subsidio
    que sería el monto total que se puede gastar. 

G. El modelo no tiene redundancia de datos.

    Falso. El modelo si tiene redundancia de datos. 
    - monto en la relación pertenece podría no estar porque indica el monto que se le da a cada beneficiario
    - en Persona se guarda nombre y en persona Fisica también. 

**4) Análisis de un modelo de E/R**

Dado el siguiente modelo E/R sobre vendedores que trabajan en locales:

![cuadro-ej4](https://github.com/annecchiniv/informatica-unlp/blob/master/3ER%20A%C3%91O/BD1/CUADROS/cuadro-ej4.jpg?raw=true)

A. En qué casos modelaría un atributo fecha _de_ingreso en la relación se_emplea –entre
Vendedor y Local - como se muestra en la variante “A”?

    En el caso donde no necesito tener un gistorial de las fechas de ingreso. 
    Solo se guarda una única fecha por local, quedaría siempre la última fecha. 

B. ¿En qué casos haría falta modelar una entidad Fecha de ingreso relacionada con la
agregación Vendedor Local como se muestra en la parte llamada B en el modelo?

    En el caso que necesite un historial de fechas de ingreso.

C. ¿Qué se está modelando con Horario cuando está la agregación? Indíquelo agregando la cardinalidad correspondiente.

    Se modela el horario de cada vendedor en cada local. 
    - c1 si fuera (1,N) el modelo indicaria que un vendedor en un local puede trabajar en 1 o más horarios.
    - c2 si fuera (1,1) el modelo indicaria que en un horario trabaja un unico vendedor. 
    - c2 si fuera (1,N) el modelo indicaria que en un horario trabajan 1 o más vendedores.
    - c2 si fuera (1,N) el modelo indicaria que existe un horario sin nadie trabajando. 
