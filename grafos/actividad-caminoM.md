**Actividad Práctica grafos - Miercoles 8:30 - 09/12/2020**

Camino con “M”

Mariano está planeando su siguiente viaje para después de la pandemia. Mariano organiza su viaje con una peculiaridad: sólo puede pasar por ciudades cuyo nombre empiece con la 
letra “M”. En este viaje empieza su recorrido en Mar del Plata y su destino final es Munich.
Se pide implementar el método obtenerRecorrido dentro de la clase recorridoM que devuelva el camino más corto entre el origen y el destino que cumpla la condición que el nombre de
todas las ciudades por las que pasa debe comenzar con la letra “M”. Para el siguiente ejemplo:

[!caminoM](camino-m1.jpg)

Existen varios caminos entre Mar del Plata y Munich, por ejemplo:

* Mar del Plata -> Montevideo -> Barcelona -> Munich
* Mar del Plata -> Buenos Aires -> Barcelona -> Munich
* Mar del Plata -> Montevideo -> Madrid -> Monaco -> Munich
* Mar del Plata -> Montevideo -> Madrid -> Munich

Los dos últimos caminos son los únicos que cumplen la condición de que todos los nombres de las ciudades comienzan con “M”. 

Entre estos el último es el más corto, por lo cual el camino a retornar para este ejemplo es: **Mar del Plata -> Montevideo -> Madrid -> Munich**
