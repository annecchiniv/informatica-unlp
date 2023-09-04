**1) Cuadros**

![cuadro-ej1](https://github.com/annecchiniv/informatica-unlp/blob/master/3ER%20A%C3%91O/BD1/cuadro1-ej1.jpg?raw=true)

    Hay 2 relaciones con el mismo nombre “expuesto" y esto es un error ya que 
    no pueden haber dos relaciones/entidades con el mismo nombre 
    por lo tanto habría que modificar el nombre de alguna.
    Entonces corrijo el error y cambio a "expone" el nombre de la relación "expuesto" 
    entre la agregación y la entidad periodo
    
![cuadro1.2-ej1](https://github.com/annecchiniv/informatica-unlp/blob/master/3ER%20A%C3%91O/BD1/cuadro1.2-ej1.jpg?raw=true)

a. En este modelo cada período de exposición contiene múltiples cuadros en museos. ¿Qué
parte del modelo indica esto? ¿Cómo la modificaría para que cada período fuese exclusivo de
cada cuadro expuesto en un museo?

    ¿Qué parte del modelo indica esto?
    La parte del modelo que indica que cada período de exposición 
    contiene múltiples cuadros en museos es la cardinalidad (1,N) 
    de la relación Expone del lado de la agregación.  
    
![cuadro1.3-ej1](https://github.com/annecchiniv/informatica-unlp/blob/master/3ER%20A%C3%91O/BD1/cuadro1.3-ej1.jpg?raw=true)
    
    ¿Cómo la modificaría para que cada período fuese exclusivo de cada cuadro expuesto en un museo?
    Modificaria la cardinalidad antes mencionada a (1,1) 
    

b. Si los cuadros se expusieran en un solo período dentro de cada museo ¿cómo ajustaría el modelo para reflejar esto?

    Cambiaria la otra cardinalidad (del lado de Periodo) a (1,1) 

c. Ajuste el modelo para representar museos de dos tipos: de **arte contemporáneo**, con fecha de inauguración, país y director;  y de **arte en general**, del cual se conoce una fecha estimada de inauguración, país, director y datos históricos. De los datos históricos se registra un año y una descripción histórica, por ejemplo que una pintura famosa se exhibió por primera vez allí en un año determinado.

