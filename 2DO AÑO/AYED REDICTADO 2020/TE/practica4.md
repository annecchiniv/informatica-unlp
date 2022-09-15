**Ejercicio 1**

Debido a un error en la actualización de sus sistemas, el banco AyED perdió la información del
estado de todas sus cuentas. Afortunadamente logran recuperar un backup del día anterior y
utilizando las transacciones registradas en las últimas 24hrs podrán reconstruir los saldos. Hay poco
tiempo que perder, el sistema bancario debe volver a operar lo antes posible.
Las transacciones se encuentran agrupadas en consultas, una consulta cuenta con un valor y un
rango de cuentas consecutivas a las que hay que aplicar este cambio, por ejemplo la consulta
(333..688 = 120) implica sumar $120 a todas las cuentas entre la número 333 y la número 688
(inclusive). Entonces, la recuperación de los datos consiste en aplicar todas las consultas sobre el
estado de las cuentas recuperado en el backup del día anterior.
El equipo de desarrollo se pone manos a la obra y llega a una solución rápidamente. Toman cada
consulta y recorren el rango de cuentas aplicando el valor correspondiente, como muestra el
siguiente algoritmo.

        Consultas.comenzar()
        While(!consultas.fin()){
                Consulta = consultas.proximo();
                for(i = consulta.desde; i < consulta.hasta; i++){
                        cuenta[i] = cuenta[i] + consulta.valor;
                }
        }

Escriben la solución en pocos minutos y ponen en marcha el proceso de recuperación. Enseguida se
dan cuenta que el proceso va a tardar muchas horas en finalizar, son muchas cuentas y muchos
movimientos, la solución aunque simple es ineficiente. Luego de discutir varias ideas llegan a una
solución que logra procesar toda la información en pocos segundos.

a.- Para que usted pueda experimentar el tiempo que demora cada uno de los dos algoritmos, lo
ponemos a vuestra disposición. Usted debe ejecutar cada uno de los algoritmo, con distinta cantidad
de elementos y complete la tabla. Luego haga la gráfica para comparar los tiempos de ambos
algoritmos. Tenga encuenta que el algoritmo posee dos constantes CANTIDAD_CUENTAS y
CANTIDAD_CONSULTAS, sin embargo, por simplicidad, ambas toman el mismo valor. Solo necesita
modificar CANTIDAD_CUENTAS 

![cuadro-completado](https://github.com/annecchiniv/informatica-unlp/blob/master/2DO%20A%C3%91O/AYED%20REDICTADO%202020/TE/cuadro-ej1.jpg?raw=true)
![grafico](https://github.com/annecchiniv/informatica-unlp/blob/master/2DO%20A%C3%91O/AYED%20REDICTADO%202020/TE/grafico-ej1.jpg?raw=true)

b.- ¿Por qué procesarMovimientos es tan ineficiente? Tenga en cuenta que pueden existir millones
de movimientos diarios que abarquen gran parte de las cuentas bancarias.

        El primer algoritmo es tan ineficiente porque se puede ver que tiene 2 for anidados. Esto indicaría O(n^2).
        En cambio, el segundo algoritmo tiene O(n). Tiene 2 for que no estan anidados. 

c.- ¿En qué se diferencia procesarMovimientosOptimizado? Observe las operaciones que se
realizan para cada consulta.

        procesarMovimientosOptimizado se diferencia porque recorre todas las cuentas y consultas una única vez.
        El otro algoritmo recorre todas las cuentas y consultas varias veces. 

Aunque los dos algoritmos se encuentran explicados en los comentarios, no es necesario entender
su funcionamiento para contestar las preguntas
