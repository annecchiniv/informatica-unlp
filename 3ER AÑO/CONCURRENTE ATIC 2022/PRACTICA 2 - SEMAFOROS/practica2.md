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
