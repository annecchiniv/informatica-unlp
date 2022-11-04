*Ejercicios corregidos (preg igual, hay muchas maneras de hacerlos)*

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
    
    sem det=1; --> asi solamente UNA persona puede usar el detector. 
    no puede estar en 0 xq se demorarian todos esperando a entrar a la SC.   
    
    
    b. Modifique su solución para el caso que haya tres detectores. 
    
    sem det=3; --> puede atender a 3 personas   
    
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
    
    Aca tambien podría usarse push(cola, inst) y pop(cola, inst) en vez de inst = cola.push(); y cola.pop(inst).
    Recordar que es pseudocodigo, creo que en la teoria lo hacen de la primer manera. 
    
3. Suponga que existe una BD que puede ser accedida por 6 usuarios como máximo al mismo tiempo. 
Además, los usuarios se clasifican como usuarios de prioridad alta y usuarios de prioridad baja. Por último, la BD tiene la siguiente restricción:
    * no puede haber más de 4 usuarios con prioridad alta al mismo tiempo usando la BD
    * no puede haber más de 5 usuarios con prioridad baja al mismo tiempo usando la BD
    
   Indique si la solución presentada es la más adecuada. Justifique la respuesta. 

   [![tabla](https://github.com/annecchiniv/informatica-unlp/blob/master/3ER%20A%C3%91O/CONCURRENTE%20ATIC%202022/PRACTICA%202%20-%20SEMAFOROS/cuadro-ej3.PNG)]()
   
   
        No, no es la mas adecuada. Seria mejor que P(sem) este después de P(baja) o P(alta) debido a que accedo a la BD 
        antes de saber si puedo acceder segun mi prioridad. 
        Se podría generar una demora innecesaria en el caso de haber tomado el acceso a la BD sin poder hacerlo con mi prioridad.
        
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
        
4. Existen N personas que deben imprimir un trabajo cada una. Resolver cada ítem usando
semáforos:

        a) Implemente una solución suponiendo que existe una única impresora compartida por todas las personas, 
        y las mismas la deben usar de a una persona a la vez, sin importar el orden. 
        Existe una función Imprimir(documento) llamada por la persona que simula el uso de la impresora. 
        Sólo se deben usar los procesos que representan a las Personas.

        sem imp:=1;
        
        Process Persona[id:0..N]{
            text doc;
            P(imp);
                Imprimir(doc);
            V(imp);
        }

        b) Modifique la solución de (a) para el caso en que se deba respetar el orden de llegada.
        
        Como se debe respetar el orden de llegada tengo que usar una estructura que me permita ordenar y es la cola. 
        Hay que protegerla.
        Usar passing the baton
        
        sem mutex:=1, espera[N]:=([N]:=0);
        Cola cola;
        bool libre:=true;
        
        Process Persona[id:0..N]{
            text doc; 
            int aux;
            while(true){ --> creo q no es necesario el while true
                P(mutex);
                if(libre){
                    libre:=false;
                    V(mutex);
                }
                else{
                    push(cola, id);
                    V(mutex);
                    P(espera[id]);
                }
                Imprimir(doc);
                P(mutex);
                if(not empty(cola)){
                    aux:= pop(cola,id);
                    V(espera[aux]);
                }
                else
                    libre:=true;
                V(mutex);
            }
        }
      
        Utilizo semáforos privados xq cuando se despierta a alguien, el unico que se tiene que enterar es el 1ero
        en la fila y decirle en ese instante que la fotocopiadora esta libre, el resto de los que esperan o que
        ni siquiera llegaron no se deben enterar q el recurso compartido esta libre. 
        Esta es la unica manera de despertar a UN solo proceso. 
      
        c) Modifique la solución de (a) para el caso en que se deba respetar estrictamente el orden dado por 
        el identificador del proceso (la persona X no puede usar la impresora hasta que no haya terminado 
        de usarla la persona X-1).
        
        sem mutex:=1, espera[N]:=([N]:=0);
        int sig:=1;
        
        Process Persona[id:0..N]{
            text doc;
            P(mutex);
            if(sig != id){
                V(mutex); --> primero libero y luego me duermo en mi semaforo
                P(espera[id]);
            }
            else
                V(mutex);
            Imprimir(doc);
            P(mutex);
            if(sig < N)
                sig++;
            else
                sig:=1;
            V(mutex);
            V(espera[sig]);
        }

        d) Modifique la solución de (b) para el caso en que además hay un proceso Coordinador que le indica a 
        cada persona que es su turno de usar la impresora.
        
        sem mutex:=1, aviso:=0, espera[N]=([N]:=0);
        Cola cola;
        
        Process Persona[id:0..N]{
            text doc;
            P(mutex);
            push(cola,id);
            V(mutex);
            V(aviso);
            P(espera[id]);
            Imprimir(doc);
            V(termine);
        }
        
        Process Coordinador{
            int sig;
            while(true){
                P(aviso);
                P(mutex);
                sig:=pop(cola,id); si llego aca ya me avisaron que hay algo en la cola, por eso no se chequea
                V(mutex);
                V(espera[sig]); 
                P(termine); 
            }
        }
        
        El V(aviso) de process persona es para avisar a coordinador que hay 1 en la cola. 
        Esto es para que no se chequee todo el tiempo si hay algo generaría demora innecesaria.
        El V(termine) de process persona es para avisar a coordinador que ya termino de usar el recurso compartido
                          
        En sig:=pop(cola,id) de process coordinador si llego a este punto ya me avisaron que hay algo en la cola
        por eso no se chequea
        El V(espera[sig]) de process coordinador despierta al que sigue 
        El P(termine) de process coordinador espera a que avisen que se libera recurso compartido
    
        e) Modificar la solución (d) para el caso en que sean 5 impresoras. El coordinador le indica a la persona 
        cuando puede usar una impresora, y cual debe usar.
        
        sem mutex:=1, cual_f[N]:=([N]:=0);
        Cola cola, cola_f;
        int id_f;
        
        Process Persona[id:0..N]{
            text doc;
            P(mutex);
            push(cola, id);
            V(mutex);
            V(aviso);
            P(espera[id]);
            Imprimir(doc);
            P(mutex);
            push(cola_f, id_f);
            V(mutex);
            V(termine);
        }
        
        Process Coordinador{
            int sig, sigI;
            while(true){
                P(aviso);
                P(mutex);
                sig:=pop(cola, id);
                sigI:=pop(cola_f, id_f);
                cual_f[id]:=sigI;
                V(mutex);
                V(espera[sig]);
                P(termine);
            }
        }
        
5. Suponga que se tiene un curso con 50 alumnos. Cada alumno debe realizar una tarea y existen 10 enunciados posibles. 
Una vez que todos los alumnos eligieron su tarea, comienzan a realizarla. 
Cada vez que un alumno termina su tarea, le avisa al profesor y se queda esperando el puntaje del grupo, el cual está dado por 
todos aquellos que comparten el mismo enunciado.
Cuando un grupo terminó, el profesor les otorga un puntaje que representa el orden en que se terminó esa tarea de las 10 posibles.
Nota: Para elegir la tarea suponga que existe una función Elegir() que le asigna una tarea a un alumno 
(esta función asignará 10 tareas diferentes entre 50 alumnos, es decir, que 5 alumnos
tendrán la tarea 1, otros 5 la tarea 2 y así sucesivamente para las 10 tareas).

        sem mutex:=1, barrera:=0, cola:=1, listo:=0, esperapuntaje[10]:=([10]:=0)
        int cantA:=0, alumno_g[50], puntajes[10];
        Cola colaG;
            
        Process Alumno[id:1..50]{
            int i;
            P(mutex);
            cantA++;
            if(cantA == 50)
                for i:=1..50 loop
                    alumno_g[i]:= Elegir();
                end loop;
            V(mutex); --> siempre va antes que el P(barrera)
            P(barrera);
            //hace la tarea
            P(cola);
            push(colaG, alumno_g[id]) --> encolo el id de mi grupo
            V(cola);
            V(listo);
            P(esperapuntaje[alumno_g[id]]) --> barrera de grupo para esperar puntaje
        }
        
        Process Profesor{
            int i, idG, orden:=0, grupos[10]:=([10]:=0);
            while(true){
                P(listo); --> espera a que haya alguien q termine
                P(cola);
                idG:= pop(colaG, idG); --> saco id de alumno del grupo
                V(cola);
                
                grupos[idG]++;
                
                if(grupos[idG] == 5){ --> el grupo termino, hay 5 alumnos
                    orden++;
                    puntajes[idG]:=orden;
                    for i:=1..5 loop
                        V(esperapuntaje[idG]); --> despierto a todos los de ese grupo para dar el puntaje
                    end loop;
                }
                
            }
        }
        
6. A una empresa llegan E empleados y por día hay T tareas para hacer (T>E), una vez que
todos los empleados llegaron empezaran a trabajar. Mientras haya tareas para hacer los
empleados tomarán una y la realizarán. Cada empleado puede tardar distinto tiempo en
realizar cada tarea. Al finalizar el día se le da un premio al empleado que más tareas realizó.

        sem mutex:=1, barrera:=0, tarea:=1, cont_tarea:=1, terminaron:=1, listo:=1;
        int totalT:=T, cantE:=0, tareas[e]:=([E]:=0), empleados:=0;
        
        Process Empleado[id:1..E]{
            int i;
            P(mutex);
            cantE++;
            if(cantE == E)
                for i:=1..E loop
                    V(barrera);
                end loop;
            V(mutex);
            P(barrera);
            
            //empiezo a trabajar
            
            P(tarea);
            while(total > 0){
                totalT--;
                V(tarea);
                RealizarTarea();
                tareas[id]++;
                P(tarea);
            }
            V(tarea);
            V(listo);
            P(terminaron);
            empleados++;
            V(terminaron);
        }
        
        Process Premio{
            int ganador;
            P(listo);
            P(terminaron);
            if(finalizadas == T)
                ganador:= CalcularMaximo(tareas[E]);
            V(terminaron);
        }
        
        Observaciones:
            - No es necesario tener un proceso premio. 
            - Hay que ir incrementando la cantidad de empleados.

7. Resolver el funcionamiento en una fábrica de ventanas con 7 empleados (4 carpinteros, 1 vidriero y 2 armadores) 
que trabajan de la siguiente manera:

* Los carpinteros continuamente hacen marcos (cada marco es armando por un único
carpintero) y los deja en un depósito con capacidad de almacenar 30 marcos.

* El vidriero continuamente hace vidrios y los deja en otro depósito con capacidad para 50
vidrios.

* Los armadores continuamente toman un marco y un vidrio (en ese orden) de los
depósitos correspondientes y arman la ventana (cada ventana es armada por un único
armador).

        sem dm:=30, dv:=50, cm:=1, cv:=1;
        Cola colaM, colaV;
        
        Process Carpintero[id:1..4]{
            Marco m;
            
            while(true){
                m:=HacerMarco();
                P(dm);
                P(cm);
                push(colaM, m);
                V(cm);
                V(marco); --> aviso que esta listo el marco
            }
        }
        
        Process Vidriero{
            Vidrio v;
            
            while(true){
                v:= HacerVidrio();
                P(dv);
                P(cv);
                push(colaV, v);
                V(cv);
                V(vidrio); 
            }
        }
        
        Process Armador[id:1..2]{
            Marco m;
            Vidrio v;
        
            while(true){
                P(marco);
                P(cm);
                m:=pop(colaM, m);
                V(cm);
                P(vidrio);
                P(cv);
                v:=pop(colaV, v);
                V(cv);
                ArmarVentana(m, v);
                GuardarVentana();
            }
        }
        
8. A una cerealera van T camiones a descargarse trigo y M camiones a descargar maíz. 
Sólo hay lugar para que 7 camiones a la vez descarguen, pero no pueden ser más de 5 del mismo tipo de cereal. 
Nota: no usar un proceso extra que actué como coordinador, resolverlo entre los camiones.

        sem tot:=7, trigo:=5, maiz:=5; --> se inicializan en 5 porque mas no pueden ser del MISMO tipo
        
        Process CamionT[id:0..T]{
            P(trigo);
            P(tot); --> descuento del total de camiones que hay a la vez
            //Descargando trigo
            V(tot);
            V(trigo);
        }

        Process CamionM[id:0..M]{
            P(maiz);
            P(tot);
            //Descargando maiz
            V(tot);
            V(maiz);
        }
        
9. En un curso hay dos profesores que toman examen en forma oral, el profesor A llama a los alumnos de acuerdo con el orden de llegada, 
mientras que el profesor B llama al de menor número de alumno (que esté esperando ser llamado para rendir). 
Existen N alumnos que llegan y se quedan esperando hasta ser llamados para rendir, luego de que uno de los dos
profesores lo atiende, se va. Indicar si la siguiente solución realizada con semáforo resuelve lo pedido. Justificar la respuesta.

        string estado[N] = ([N], “Esperando” )
        queue colaA, colaB
        sem llegoA, llegoB = 0
        sem esperando[N] = ([N], 0)
        sem mutexA, mutexB = 1
        
        Alumno[i: 1..N]{ 
         P(mutexA)
         push(colaA, i)
         V(mutexA)
         V(llegoA)
         P(mutexB)
         push(colaB, i)
         V(mutexB)
         V(llegoB)
         P(esperando[i])
         if (estado[i] == “A”)
            //Interactúa con el Prof A//
         else
            //Interactua con el Prof B//
         P(esperando[i])
        }
        
        Profesor A::{ 
         int idAlumno;
         while (true){
             P(llegoA)
             P(mutexA)
             idAlumno = pop(colaA)
             V(mutexA)
             if(estado[idAlumno] == “Esperando”){ 
                 estado[idAlumno] = “A”
                 V(esperando[idAlumno])
                 //Se toma el examen//
                 V(esperando[idAlumno])
             }
         }
        }
        
        Profesor B::{ 
         int idAlumno;
         while (true){ 
             P(llegoB)
             P(mutexB)
             idAlumno = popAleatorio(colaB)
             V(mutex(B))
             if(estado[idAlumno] == “Esperando”){
                estado[idAlumno] = “B”
                V(esperando[idAlumno])
                //Se toma el examen//
                V(esperando[idAlumno])
             }
         }
        }

        No, no se resuelve lo pedido. Se encola al alumno en 2 colas distintas. Se debería encolar en una sola y que los 2 profesores
        cheequen esa cola.
        No se si esta bien este ejercicio. 
        
10.En un vacunatorio hay un empleado de salud para vacunar a 50 personas. El empleado de
salud atiende a las personas de acuerdo con el orden de llegada y de a 5 personas a la vez. Es
decir, que cuando está libre debe esperar a que haya al menos 5 personas esperando, luego
vacuna a las 5 primeras personas, y al terminar las deja ir para esperar por otras 5. Cuando ha
atendido a las 50 personas el empleado de salud se retira. Nota: todos los procesos deben
terminar su ejecución; asegurarse de no realizar Busy Waiting; suponga que el empleado tienen
una función VacunarPersona() que simula que el empleado está vacunando a UNA persona. 
        
*Este ejercicio no esta terminado*
        
        int atendidos:=0;
        bool libre:=true;
        
        Process Empleado{
            int i, grupo:=0;
            
            while(atendidos < 50){
                P(mutex);
                if(libre){
                    for i:=1..5 loop
                        P(llegada);
                        P(cola);
                        id:= pop(c, id);
                        V(cola);
                        VacunarPersona(id);
                        V(espera[id]);
                    end loop;
                }
                else
            
            }
        }
        
        Process Persona[id:1..50]{
            P(cola);
            push(c,id);
            V(cola);
            V(llegada);
            P(esperaV[id]);
            Irse();
        }

11 sin hacer :(


        
