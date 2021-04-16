```
public ListaGenerica<String> obtenerRecorrido(Grafo<String> grafo, String ciudad1, String ciudad2){
  
    ListaGenerica<String> ciudades = new ListaEnlazadaGenerica<String>();	
    ListaGenerica<Vertice<String>> vertices = grafo.listaDeVertices();
    boolean[] marca = new boolean[grafo.listaDeVertices().tamanio()+1];
    boolean encontre = false; //buscar primera ciudad -> origen
    Vertice<String> vact = null;
    
    vertices.comenzar();
    while(!vertices.fin() && !encontre){ //mientras no termine de recorrer los vertices y no encuentre la ciudad1
        vact = vertices.proximo();  
        if(vact.dato().equals(ciudad1)) //pregunto si encontre ciudad1 para que exista camino 
            encontre=true;
    }
    if(encontre) {
      ListaGenerica<String> minimos = new ListaEnlazadaGenerica<String>(); //camino minimo actual
		  int min = Integer.MAX_VALUE;
		  min = obtenerRecorrido(grafo,vact,marca,ciudad2,ciudades,minimos, min);
		  System.out.println(min);
		
    }
  return ciudades;
}
	
private int obtenerRecorrido(Grafo<String> grafo, Vertice<String> vertice, boolean[]marca, String destino, ListaGenerica<String> ciudades, ListaGenerica<String> minimos, int min) {
	marca[vertice.getPosicion()] = true; //marco como visitado
	minimos.agregarFinal(vertice.dato());
	ListaGenerica<Arista<String>> ady = grafo.listaDeAdyacentes(vertice);
	Arista<String> arista = null;
	ady.comenzar();
	while((!ady.fin() && !vertice.dato().equals(destino))) { //busca adyacentes hasta llegar a destino, recorre todos los posibles caminos
		arista = ady.proximo(); 
		if(!marca[arista.verticeDestino().getPosicion()]){ //si no lo visite
			if(arista.verticeDestino().dato().startsWith("M")) { //if(arista.verticeDestino().dato().charAt(0) == 'M')
				min = obtenerRecorrido(grafo,arista.verticeDestino(),marca,destino,ciudades,minimos, min); 
			}
		}
	}
	if((minimos.elemento(minimos.tamanio()).equals(destino)) && min > minimos.tamanio()) { //si encontre el destino actualizo datos
		min = minimos.tamanio();
		while(!ciudades.esVacia()) //x si ya tenia algo, un camino viejo	
			ciudades.eliminarEn(ciudades.tamanio()); //elimino 
			for(int i=1; i <= minimos.tamanio();i++)
				ciudades.agregarFinal(minimos.elemento(i)); //a la lista final de caminos le voy agregando el nuevo camino minimo
			
	}
	minimos.eliminarEn(minimos.tamanio()); 
	marca[vertice.getPosicion()] = false; // desmarco porque haber otros caminos que pasen por ese vertice 
	return min;
}
```
