*Ejercicios corregidos (tomar con pinzas)*

1. Implementar el acceso a una base de datos de solo lectura que puede atender a lo sumo 5 consultas simultáneas.

        Process Proceso[id:0..N-1]{
          BD.Entrar();
          //UsarBD
          BD.Salir();
        }
        
        Monitor BD{
            int disponible:=5; --> hay 5 lugares
            cond espera;

            Procedure Entrar(){
              while(disponible==0) --> disponible == 0 no puedo entrar a la BD
                wait(espera); --> espero
              disponible--;
            }

            Procedure Salir(){
              disponible++;
              signal(espera); --> despierto
            }
        }
        
2. Existen N personas que deben fotocopiar un documento cada una. Resolver cada ítem usando monitores:

        a) Implemente una solución suponiendo que existe una única fotocopiadora compartida por todas las personas, 
        y las mismas la deben usar de a una persona a la vez, sin importar el orden. 
        Existe una función Fotocopiar() que simula el uso de la fotocopiadora.
        Sólo se deben usar los procesos que representan a las Personas (y los monitores que sean necesarios).

        Process Persona[id:0..N-1]{
          Fotocopiadora.PasarAFotocopiar();
        }
        
        Monitor Fotocopiadora{
          Procedure PasarAFotocopiadora(){
            Fotocopiando();
          }
        }

        b) Modifique la solución de (a) para el caso en que se deba respetar el orden de llegada.

        Process Persona[id:0..N-1]{
          Fotocopiadora.Pasar();
          Fotocopiar();
          Fotocopiadora.Salir();
        }

        Monitor Fotocopiadora{
          cond cola;
          int espera:=0;
          bool libre:=true;
          
          Procedure Pasar(){
            if(not libre){
              espera++;
              wait(cola);
            }
            else
              libre:=false; --> esta disponible entonces la ocupo
          }
        
          Procedure Salir(){
            if(espera>0){
              signal(cola);
              espera--;
            }
          }
          else 
            libre:=true;
        }

        c) Modifique la solución de (b) para el caso en que se deba dar prioridad de acuerdo a la
        edad de cada persona (cuando la fotocopiadora está libre la debe usar la persona de
        mayor edad entre las que estén esperando para usarla).
        
        Process Persona[id:0..N-1]{
          Fotocopiadora.Pasar(id,edad);
          Fotocopiando();
          Fotocopiadora.Salir();
        }

        Monitor Fotocopiadora{
          cond colaEspera[N];
          colaOrdenada filaE;
          bool libre:=true;
          int idAux, espera:=0;

          Procedure Pasar(idP, edad: IN int){
            if(not libre){
              insertar(filaE, idP, edad);
              espera++;
              wait(colaEspera[idP]);
            } 
            else 
              libre:=false;
          }
          
          Procedure Salir(){
            if(espera>0){
              espera--;
              sacar(filaE, idAux);
              signal(colaEspera[idAux]);
            }
            else 
              libre:=true;
          }
        }

        d) Modifique la solución de (a) para el caso en que se deba respetar estrictamente el orden
        dado por el identificador del proceso (la persona X no puede usar la fotocopiadora
        hasta que no haya terminado de usarla la persona X-1).
        
        Process Persona[id:0..N-1]{
          Fotocopiadora.Pasar(id);
          Fotocopiando();
          Fotocopiadora.Salir(id);
        }
        
        Monitor Fotocopiadora{
          cond colaEspera[N];
          int idAct:=1;
          
          Procedure Pasar(idP: IN int){
            if(idP <> idAct)
              wait(colaEspera[idP]);
          }
        
          Procedure Salir(idP: IN int){
            if(idAct < N){
              idAct++;
              signal(colaEspera[idAct]);
            }
          }        
        }

        e) Modifique la solución de (b) para el caso en que además haya un Empleado que le indica
        a cada persona cuando debe usar la fotocopiadora.

        Process Persona[id:0..N-1]{
          Admin.Llegada();
          Fotocopiadora.Utilizar();
          Fotocopiadora.Termimo();
        }
        
        Process Empleado{
          while(true){
            Admin.Proximo();
            Fotocopiadora.EsperaTurnoPersona();
          }
        }
        
        Monitor Admin{
          bool eLibre:=true;
          int espera:=0;
          cond colaEspera;
          
          Procedure Llegada(){
            if(not eLibre){
              espera++;
              wait(colaEspera);
            }
            else
              eLibre:=false;
          }
          
          Procedure Proximo(){
            if(espera>0){
              espera--;
              signal(colaEspera);
            }
            else
              eLibre:=true;
          }
        }        
  
        Monitor Fotocopiadora{
          cond emp;
          bool termine:=false;
          
          Procedure Utilizar(){
            Fotocopiar();
          }
          
          Procedure Termino{
            termino:=true;
            signal(emp); --> despierto a empleado para q diga quien sigue
          }
        
          Procedure EsperaTurnoPersona(){
            if(not termine)
              wait(emp); --> empleado espera para dar turno
            termino:=false;
          }
        
        }

        f) Modificar la solución (e) para el caso en que sean 10 fotocopiadoras. El empleado le
        indica a la persona cuando puede usar una fotocopiadora, y cual debe usar. 
        
        sin hacer :(
        
3. En un corralón de materiales hay un empleado que debe atender a N clientes de acuerdo al orden de llegada. 
Cuando un cliente es llamado por el empleado para ser atendido, le da una lista con los productos que comprará, 
y espera a que el empleado le entregue el comprobante de la compra realizada.

*Es parecido al de la explicacion practica de monitores de las secuencias de ADN*

        Process Cliente[id:0..N-1]{
          Admin.Llegada()
          Venta.Comprar(lista,id,c)
        }
        
        Process Empleado{
          Admin.Proximo();
          Venta.Atender(lista, comprobante);
        }
        
        Monitor Admin{
          bool eLibre:=true;
          int espera:=0;
          cond colaE;
          
          Procedure Llegada(){
            if(not eLibre){
              espera++;
              wait(colaE);
            }
            else eLibre:=false;
          }
          
          Procedure Proximo(){
            if(espera>0){
              espera--;
              signal(colaE);
            }
            else eLibre:=true;
          }
        }
        
        Monitor Venta{
          bool eLibre:=true;
          cond emple, cli[N], comprobantesE[N];
          int idAct, hayClientes:=0;
          text comprobantes[N], L;
          
          Procedure Comprar(lista: IN text, id: IN int, c: OUT text){
            idAct:=id;
            L:=lista;
            if(not eLibre){
              hayClientes++;
              wait(cli[idAct]);
            }
            else{
              eLibre:=false;
              signal(emple);
              darLista(L);
              wait(comprobantesE[idAct]);
              c:=comprobantes[id];
            }
          }
          
          Procedure Atender(lista: IN text, comprobante: OUT text){
            if(hayClientes>0){
              hayClientes--;
              signal(cli[idAct]);
              Atendiendo(L);
              GenerarC(comprobantes[idAct]);
              signal(comprobantesE[idAct]);
            }
            else{
              eLibre:=true;
              wait(emple);
            }
          }
        }
        
4. Suponga una comisión con 50 alumnos. Cuando los alumnos llegan forman una fila, una vez que están los 50 en la fila 
el jefe de trabajos prácticos les entrega el número de grupo (número aleatorio del 1 al 25) de tal manera que 
dos alumnos tendrán el mismo número de grupo (suponga que el jefe posee una función DarNumero() que devuelve en forma aleatoria 
un número del 1 al 25, el jefe de trabajos prácticos no guarda el número que le asigna a cada alumno). 
Cuando un alumno ha recibido su número de grupo comienza a realizar la práctica. Al terminar de trabajar, el alumno le avisa al jefe 
de trabajos prácticos y espera la nota. El jefe de trabajos prácticos, cuando han llegado los dos alumnos de un grupo les
devuelve a ambos la nota del GRUPO (el primer grupo en terminar tendrá como nota 25, el segundo 24, y así sucesivamente 
hasta el último que tendrá nota 1).

        Process Alumno[id:1..50]{
          Comision.Llegada();
          Practicando();
          Comision.RecibirNota(id);
        }
        
        Process JefeTPS{
          int i;
          Comision.Espera();
          Comision.FormarGrupos();
          for i:=1..25
            Comision.EntregarNota();
        }
        
        Monitor Comision{
            int cant:=0, alumnos[N], esperando:=0, termine[N]:=([N]:=0), notas[N];
            cond espera, inicio, correccion, numGrupo[N/2], esperaNotas[N/2];

            Procedure Llegada(){
              cant++;
              if(cant==50){
                signal(inicio);
              }
              wait(espera);
            }

            Procedure Espera(){
              if(cant<50){
                wait(inicio);
              }
            }

            Procedure FormarGrupos(){
              for i:=1..50 loop
                alumos[i]:=DarNumero();
              signal_all(espera); --> despierto a todos despues de dar el nro de grupo
            }

            Procedure EntregarNota(){
              int grupo;
              wait(correccion);
              grupo:=pop(colaG, idG); --> no es necesario preg por empty de la cola xq si o si habra un grupo
              notas[grupo]:=DarNota();
              signal(esperaNotas[grupo]);
            }

            Procedure RecibirNota(id: IN int){
              termine[alumnos[id]]++;
              if(termine[alumnos[id]] == 2){
                push(colaG, idG);
                signal(correccion);
              }
              wait(esperaNotas[alumnos[id]]);
            }
        }
        
5. En un entrenamiento de futbol hay 20 jugadores que forman 4 equipos (cada jugador conoce el equipo al cual pertenece 
llamando a la función DarEquipo()). Cuando un equipo está listo (han llegado los 5 jugadores que lo componen), debe enfrentarse a otro equipo que
también esté listo (los dos primeros equipos en juntarse juegan en la cancha 1, y los otros dos equipos juegan en la cancha 2). 
Una vez que el equipo conoce la cancha en la que juega, sus jugadores se dirigen a ella. 
Cuando los 10 jugadores del partido llegaron a la cancha comienza el partido, juegan durante 50 minutos, y al terminar todos los jugadores del
partido se retiran (no es necesario que se esperen para salir).

        Process Jugador[id:0..19]{
          indt idC, idE:= DarEquipo();
          
          Equipo.Llegada(idE);
          Equipo.EsperaC(idC);
          Cancha[idC].EsperaP();
        }
        
        Process Partido[id:1..2]{
          Cancha[id].Iniciar();
          delay(50 minutos); --> jugando
          Cancha[id].Terminar();
        }
        
        Monitor Equipo[id:1..4]{
          int equipos[4]:=([4]:=0), cancha[2]:=([2]:=0);
          cond esperaE[4];
          
          Procedure Llegada(idE: IN int){
            if(equipos[idE] == 5)
              wait(esperaE[idE]);
            else{
              signal_all(esperaE[idE]);
              equipos[idE]++;
            }
          }
          
          Procedure EsperaC(idC: OUT int){
            if(cancha[1]<2){
              cancha[1]++;
              idC:=1;
            }
            else
              idC:=2;
          }
        }
        
        Monitor Cancha[id:1..2]{
          int jug:=0;
          
          Procedure EsperaP(){
            jug++;
            if(jug==10)
              signal(inicio)
            wait(esperandoP);
          }
          
          Procedure Inicio(){
            if(jug<10)
              wait(inicio);
          }
          
          Procedure Terminar(){
            signal_all(esperandoP);
          }
        }

6. En una playa hay 5 equipos de 4 personas cada uno (en total son 20 personas donde cada
una conoce previamente a que equipo pertenece). Cuando las personas van llegando
esperan con los de su equipo hasta que el mismo esté completo (hayan llegado los 4
integrantes), a partir de ese momento el equipo comienza a jugar. El juego consiste en que
cada integrante del grupo junta 15 monedas de a una en una playa (las monedas pueden ser
de 1, 2 o 5 pesos) y se suman los montos de las 60 monedas conseguidas en el grupo. Al
finalizar cada persona debe conocer el monto total juntado por su grupo. Nota: maximizar
la concurrencia. Suponga que para simular la búsqueda de una moneda por parte de una
persona existe una función Moneda() que retorna el valor de la moneda encontrada.

        Process Jugador[id:0..19]{
          int idE, monto:=0;
          
          Equipo[idE].Llegada();
          for i:=1 to 15 loop
            monto:=monto + Moneda();
          Equipo[idE].EsperaTotal(monto,totalE);
        }
        
        Monitor Equipo[id:1..5]{
          int cant:=0, total:=0, termino:=0;
          cond esperaE, esperaT;
          
          Procedure Llegada(){    
            cant++;
            if(cant==4)                           
              signal_all(esperaE);
            else
              wait(esperaE);
          }
          
          o tambien puede hacerse. Puede q el ultimo no se duerma
          if(cant<4)
            wait(esperaE)
          else
            signal_all(esperaE)
        
          Procedure EsperaTotal(monto: IN int, totalE: out int){
            total:=total+monto;
            termino++;
            if(termino==4){
              signal_all(esperaT);
              totalE:=total;
            }
            else
              wait(esperaT);
          }
          
          
  7. Se debe simular una maratón con C corredores donde en la llegada hay UNA máquinas
expendedoras de agua con capacidad para 20 botellas. Además existe un repositor
encargado de reponer las botellas de la máquina. Cuando los C corredores han llegado al
inicio comienza la carrera. Cuando un corredor termina la carrera se dirigen a la máquina
expendedora, espera su turno (respetando el orden de llegada), saca una botella y se retira. Si
encuentra la máquina sin botellas, le avisa al repositor para que cargue nuevamente la
máquina con 20 botellas; espera a que se haga la recarga; saca una botella y se retira. Nota:
maximizar la concurrencia; mientras se reponen las botellas se debe permitir que otros
corredores se encolen. 

        Process Corredor[id:0..C]{
          int cantB:=20;
          Carrera.Inicio();
          Corriendo();
          Carrera.EsperaMaquina();
          Carrera.TomarBotella();
          Irse();
        }
        
        Process Repositor{
          Carrera.Reponer();
        }
        
        Monitor Carrera{
            cond iniciar, maquina, reposicion;
            int cantC:=0, esperaM, botellas:=20;
            bool libre:=true;

            Procedure Inicio(){
              cantC++;
              if(cantC == C)
                signal_all(iniciar);
              else
                wait(iniciar);
            }

            Procedure EsperaMaquina(){
              if(not libre){
                esperaM++;
                wait(maquina);
              }
              else libre:=false;
            }

            Procedure TomarBotella(){
              if(botellas>0)
                botellas--;
              else
                signal(reposicion);

              if(esperaM>0){
                signal(maquina);
                esperaM--;
              }
              else libre:=true;
            }

            Procedure Reponer(){
              if(botellas==0)
                botellas:=20;
              else
                wait(reposicion);
            }
        }
        
        
        
