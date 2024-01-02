**1) Cuadros**

![cuadro 1](https://github.com/annecchiniv/informatica-unlp/blob/master/3ER%20A%C3%91O/BD1/CUADROS/cuadro%201.jpg)

    Hay 2 relaciones con el mismo nombre “expuesto" y esto es un error ya que 
    no pueden haber dos relaciones/entidades con el mismo nombre 
    por lo tanto habría que modificar el nombre de alguna.
    Entonces corrijo el error y cambio a "expone" el nombre de la relación "expuesto" 
    entre la agregación y la entidad periodo
    
![cuadro 1.2](https://github.com/annecchiniv/informatica-unlp/blob/master/3ER%20A%C3%91O/BD1/CUADROS/cuadro%201.2.jpg)

A. En este modelo cada período de exposición contiene múltiples cuadros en museos. ¿Qué
parte del modelo indica esto? ¿Cómo la modificaría para que cada período fuese exclusivo de
cada cuadro expuesto en un museo?

    ¿Qué parte del modelo indica esto?
    La parte del modelo que indica que cada período de exposición 
    contiene múltiples cuadros en museos es la cardinalidad (1,N) 
    de la relación Expone del lado de la agregación.  
    
![cuadro 1.3](https://github.com/annecchiniv/informatica-unlp/blob/master/3ER%20A%C3%91O/BD1/CUADROS/cuadro%201.3.jpg)
    
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

![cuadro 3](https://github.com/annecchiniv/informatica-unlp/blob/master/3ER%20A%C3%91O/BD1/CUADROS/cuadro%203.jpg)

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

![cuadro 4](https://github.com/annecchiniv/informatica-unlp/blob/master/3ER%20A%C3%91O/BD1/CUADROS/cuadro%204.jpg)

A. En qué casos modelaría un atributo fecha _de_ingreso en la relación se_emplea –entre
Vendedor y Local - como se muestra en la variante “A”?

    En el caso donde no necesito tener un gistorial de las fechas de ingreso. 
    Solo se guarda una única fecha por local, quedaría siempre la última fecha. 

B. ¿En qué casos haría falta modelar una entidad Fecha de ingreso relacionada con la
agregación Vendedor Local como se muestra en la parte llamada B en el modelo?

    En el caso que necesite un historial de fechas de ingreso.

C. ¿Qué se está modelando con Horario cuando está la agregación? Indíquelo agregando la cardinalidad correspondiente.

    Se modela el horario de cada vendedor en cada local. 

![cuadro 4.1](https://github.com/annecchiniv/informatica-unlp/blob/master/3ER%20A%C3%91O/BD1/CUADROS/cuadro%204.2.jpg)
    
    - c1 si fuera (1,N) el modelo indicaria que un vendedor en un local puede trabajar en 1 o más horarios.
    - c2 si fuera (1,1) el modelo indicaria que en un horario trabaja un unico vendedor. 
    - c2 si fuera (1,N) el modelo indicaria que en un horario trabajan 1 o más vendedores.
    - c2 si fuera (1,N) el modelo indicaria que existe un horario sin nadie trabajando. 

**5) Verdadero/Falso en Transformación del modelo de E/R al modelo Relacional**

![cuadro 5](https://github.com/annecchiniv/informatica-unlp/blob/master/3ER%20A%C3%91O/BD1/CUADROS/cuadro%205.jpg)

semestre (**#semestre**, año, nro)

curso (**código**, nombre, reseña)

profesor (**cuil**, nyap, fecha_nac, fecha_ingreso)

infocurso (**idic**, fecha_comienzo, aula, día_semana, hora)

brinda (**#semestre, código**)

tiene (**#semestre, código, idic**)

dicta (idic, **cuil**)

Dada la transformación 1 a 1 del modelo de entidades y relaciones al modelo relacional,
responda si las siguientes afirmaciones son V o F:

A. La relación **brinda** tiene los atributos correspondientes y su clave está bien definida

    Verdadero porque se queda con ambas claves por la cardinalidad maxima N.

B. La relación **tiene** tiene los atributos correspondientes y su clave está bien definida

    Falso. El identificador idic no va porque es (1,1) la cardinalidad.

C. La relación **dicta** tiene los atributos correspondientes y su clave está bien definida

    Falso. La clave deberia ser idic porque es (1,N) la cardinalidad.

D. La relación **tiene** no debería existir y los identificadores de la agregación deberían estar
en **InfoCurso**.

    ????
    Falso. Si no existe, los identificadores no podrian estar en InfoCurso, se necesita si o si una relación

E. La relación **dicta** no debería existir y los atributos de Profesor deberían estar en
InfoCurso.

    Falso. Son datos propios del Profesor que no interesan guardan en la información de un curso. 



