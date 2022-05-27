1.Existen N personas que deben ser chequeadas por un detector de metales antes de poder ingresar al avión.

    a. Implemente una solución que modele el acceso de las personas a un detector (es decir si el detector está libre la persona 
    lo puede utilizar caso contrario debe esperar).

    sem det=1;                     
    Process Persona[id:0..N]{
      while(true){
        P(det);
        //Usando detector
        V(det);
      }
    }
    
    
    b. Modifique su solución para el caso que haya tres detectores. 
    
    sem det=3;                     
    Process Persona[id:0..N]{
      while(true){
        P(det);
        //Usando detector
        V(det);
      }
    }

2.Un sistema operativo mantiene 5 instancias de un recurso almacenadas en una cola, cuando un proceso necesita usar
una instancia del recurso la saca de la cola, la usa y cuando termina de usarla la vuelve a depositar.
   
    Cola cola;
    sem recurso = 5, co = 1;
    Process Proceso[id:0..N-1]{
      Instancia inst;
      while(true){
        P(recurso);
          P(co);
            inst=cola.push();
          V(co);
          //Uso instancia
          P(co);
            cola.pop(inst);
          V(co);
        V(recurso);
      }
    }
    
3. Suponga que existe una BD que puede ser accedida por 6 usuarios como máximo al mismo tiempo. 
Además, los usuarios se clasifican como usuarios de prioridad alta y usuarios de prioridad baja. Por último, la BD tiene la siguiente restricción:
    * no puede haber más de 4 usuarios con prioridad alta al mismo tiempo usando la BD
    * no puede haber más de 5 usuarios con prioridad baja al mismo tiempo usando la BD
    
   Indique si la solución presentada es la más adecuada. Justifique la respuesta. 

   [![tabla](https://github.com/annecchiniv/informatica-unlp/blob/master/3ER%20A%C3%91O/CONCURRENTE%20ATIC%202022/PRACTICA%202%20-%20SEMAFOROS/cuadro-ej3.PNG)]()

        No, porque podrian seguir pasando de alta prioridad en forma consecutiva y se encuentran en un determinado momento utilizando la BD no impediria
        que sigan pasando mas usuarios de alta prioridad por el 1er sem P(sem), quedando bloqueados luego en P(alta)
    
        Correccion: 
    
        Var 
        sem: semaphoro:=6;   
        sem: semaphoro:=4;
        sem: semaphoro:=5;
        
        Process Usuario-Alta[i:1..L]::{
            P(alta);
            P(sem);
            //Usa la BD
            V(sem);
            V(alta);
        }
    
        Process Usuario-Baja[i:1..K]::{
            P(baja);
            P(sem);
            //Usa la BD
            V(sem);
            V(baja);
        }
    
        


