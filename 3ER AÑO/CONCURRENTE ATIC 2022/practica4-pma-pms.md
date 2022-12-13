*Ejercicios corregidos (preg igual, hay muchas maneras de hacerlos)*

1. Suponga que N personas llegan a la cola de un banco. Para atender a las personas existen 2 empleados que van atendiendo de a una y por orden de llegada a las personas.

        chan llegada(int), respuesta[N](text);
        
        Process Persona[id:1..N]{
          text r;
          SEND llegada(id);
          RECEIVE respuesta[id](r);
        }
        
        Process Empleado[id:1..N]{
          int idP;
          RECEIVE llegada(idP);
          //Atender persona
          SEND respuesta[idP](resp);
        }
        
2. Se desea modelar el funcionamiento de un banco en el cual existen 5 cajas para realizar pagos. Existen P clientes que desean hacer un pago. 
Para esto, cada una selecciona la caja donde hay menos personas esperando; una vez seleccionada, espera a ser atendido. En cada caja, 
los clientes son atendidos por orden de llegada. Luego del pago, se les entrega un comprobante. Nota: maximizando la concurrencia.

        chan pago[5](int);
        chan llegada(int);
        chan clientes[c](int);
        
        Process Cliente[id:1..C]{
          int canal;
          text com;
          SEND llegada(id);
          RECEIVE clientes[id](canal);
          
          SEND pago[canal](id); //llego a canal para pagar
          
          RECEIVE comprobantes[id](com);
          SEND termine(canal);
        }
        
        Process Admin {
          int idC, min, can;
          
          while(true){
            RECEIVE termine(can); //el cliente avisa cuando se va asi se actualiza el minimo y siempre la info es "real"
            min:= calcularMin(pago[5]);
            RECEIVE llegada(idC);
            SEND clientes[idC](min);
          }
        
        }
        
        Process Caja[id:1..5]{
          int idCli; text com;
          
          RECEIVE pago[id](idCli);
          com:= GenerarComprobante();
          SEND comprobantes[idCli](com);
        }

3. Se debe modelar el funcionamiento de una casa de comida rápida, en la cual trabajan 2 cocineros y 3 vendedores, y que debe atender a C clientes. 
El modelado debe considerar que:
- Cada cliente realiza un pedido y luego espera a que se lo entreguen.
- Los pedidos que hacen los clientes son tomados por cualquiera de los vendedores y se
lo pasan a los cocineros para que realicen el plato. Cuando no hay pedidos para atender,
los vendedores aprovechan para reponer un pack de bebidas de la heladera (tardan entre
1 y 3 minutos para hacer esto).
        
