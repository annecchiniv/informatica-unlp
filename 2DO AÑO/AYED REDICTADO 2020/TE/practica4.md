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

**Ejercicio 3**

En la documentación de la clase arrayList que se encuentra en el siguiente link
https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html
Se encuentran las siguientes afirmaciones
* "The size, isEmpty, get, set, iterator, and listIterator operations run in constant time.”
* “All of the other operations run in linear time (roughly speaking)”

Explique con sus palabras por qué cree que algunas operaciones se ejecutan en tiempo constante y otras en tiempo lineal.

        Creo que las operaciones que se ejecutan en tiempo constante lo hacen así porque solo tienen que preguntar 
        o iterar una única vez. 
        Por ejemplo:
                ○ En la operación size se pide el tamaño de una estructura y no es necesario recorrerla toda para 
                obtener esa información.
                ○ En la operación isEmpty se verifica si la estructura tiene al menos un elemento, tampoco es 
                necesario verificar los demas elementos. 
        Todas las demás operaciones se ejecutan en tiempo lineral ya que en el peor caso se debe recorrer toda la 
        estructura o se itera más de una vez.
        
**Ejercicio 4**

Determinar si las siguientes sentencias son verdaderas o falsas, justificando la respuesta
utilizando notación Big-Oh.
![incisos-ej4](https://github.com/annecchiniv/informatica-unlp/blob/master/2DO%20A%C3%91O/AYED%20REDICTADO%202020/TE/incisos-ej4.jpg?raw=true)

        a) Falso. 2^n es una cota inferior a 3^n
        b) Verdadero. n es una cota superior al logaritmo en base 2 de n
        c) Falso. n^(1/2) es una cota inferior a 10^20
        d) Verdadero ya que n es una cota superior a c
           3n + 17, n < 100
           317    , n >= 100 
           317 es una constante
        e) Verdadero. n^5 es una cota superior a n^4, n y c.
        f) Verdadero, por regla de Big-Oh.
        
**Ejercicio 5**

Se necesita generar una permutación random de los n primeros números enteros. Por ejemplo [4,3,1,0,2] es una 
permutación legal, pero [0,4,1,2,4] no lo es, porque un número está duplicado (el 4) y otro no está (el 3). 
Presentamos tres algoritmos para solucionar este problema. Asumimos la existencia de un generador de números random, 
ran_int (i,j) el cual genera en tiempo constante, enteros entre i y j inclusive con igual probabilidad 
(esto significa que puede retornar el mismo valor más de una vez). 
También suponemos el mensaje swap() que intercambia dos datos entre sí. 

        public class Ejercicio4 {
                private static Random rand = new Random();
                public static int[] randomUno(int n) {
                        int i, x = 0, k;
                        int[] a = new int[n];
                        for (i = 0; i < n; i++) {
                                boolean seguirBuscando = true;
                                while (seguirBuscando) {
                                        x = ran_int(0, n - 1);
                                        seguirBuscando = false;
                                        for (k = 0; k < i && !seguirBuscando; k++)
                                        if (x == a[k])
                                        seguirBuscando = true;
                                }
                                a[i] = x;
                        }
                        return a;
                }
                
                public static int[] randomDos(int n) {
                        int i, x;
                        int[] a = new int[n];
                        boolean[] used = new boolean[n];
                        for (i = 0; i < n; i++) used[i] = false;
                        for (i = 0; i < n; i++) {
                                x = ran_int(0, n - 1);
                                while (used[x]) x = ran_int(0, n - 1);
                                a[i] = x;
                                used[x] = true;
                        }
                        return a;
                }
                
                public static int[] randomTres(int n) {
                        int i;
                        int[] a = new int[n];
                        for (i = 0; i < n; i++) a[i] = i;
                        for (i = 1; i < n; i++) swap(a, i, ran_int(0, i - 1));
                        return a;
                }
                
                private static void swap(int[] a, int i, int j) {
                        int aux;
                        aux = a[i]; a[i] = a[j]; a[j] = aux;
                }
                
                /** Genera en tiempo constante, enteros entre i y j con igual probabilidad.*/
                
                private static int ran_int(int a, int b) {
                        if (b < a || a < 0 || b < 0) throw new IllegalArgumentException("Parametros invalidos");
                        return a + (rand.nextInt(b - a + 1));
                }
                
                public static void main(String[] args) {
                        System.out.println(Arrays.toString(randomUno(1000)));
                        System.out.println(Arrays.toString(randomDos(1000)));
                        System.out.println(Arrays.toString(randomTres(1000)));
                }
               
        }





           

