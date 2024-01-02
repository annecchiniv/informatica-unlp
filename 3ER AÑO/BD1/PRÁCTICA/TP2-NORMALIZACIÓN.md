# Parte 1

**Para los esquemas propuestos en cada ejercicio aplicar y explicar el proceso de normalización visto en la teoría. Todos los esquemas ya se encuentran en 1FN.**

## 1) MAPAS PUBLICADOS

### Indicar la opción correcta

Dado el siguiente esquema:

MapasPublicados (idMapa, proyección, escalaMapa, idSitioWeb, dominioSitioWeb,
especialidadSitioWeb, dueñosSitioWeb, fechaPublicaciónMapa, valorPublicación)

Donde:
- A un sitio web se le cobra un valor (“valorPublicación”) por cada fecha (“fechaPublicaciónMapa”) en la cual publique un mapa.
- Un sitio web puede tener varios dueños (“dueñosSitioWeb”).
- Un sitio web posee un único dominio (“dominioSitioWeb”).
- El identificador de un mapa (“idMapa”) es único.
- El identificador de un sitio web (“idSitioWeb”) es único.
- Un mapa se genera con una proyección y a una escala.
- “especialidadSitioWeb” es la especialidad de un sitio.

Seleccione la frase que considera verdadera
- El esquema tiene una clave candidata
- El esquema tiene más de una clave candidata

## Resolución

dfs: 

- df1: dominioSitioWeb —> idSitioWeb, especialidadSitioWeb
- df2: idSitioWeb —> dominioSitioWeb, especialidadSitioWeb
- df3: proyección, escalaMapa —> idMapa
    - idMapa —> proyeccion, escalaMapa
- df4: idSitioWeb, fechaPublicacionMapa, idMapa —> valorPublicacion
- df5: dominioSitioWeb, fechaPublicacionMapa, idMapa —> valorPublicacion
- df: dueñosSitioWeb —> idSitioWeb
    - NO LE DOY BOLA X AHORA porque dice que puede tener MUCHOS y es multivaluado

ccs: 

- cc1: idSitioWeb, proyeccion, escalaMapa, fechaPublicacionMapa, dueñosSitioWeb
    - idSitioWeb, idMapa, fechaPublicacionMapa, dueñosSitioWeb
- cc2: dominioSitioWeb, proyeccion, escalaMapa, fechaPublicacionMapa, dueñosSitioWeb
    - dominioSitioWeb, idMapa, fechaPublicacionMapa, dueñosSitioWeb

Seleccione la frase que considera verdadera
- El esquema tiene una clave candidata
- El esquema tiene más de una clave candidata ✅

**Correcion** 
```
El esquema tiene más de una clave candidata porque tengo 2 formas de identificar un mismo sitio web, por idSitioWeb o dominioSitioWeb. 
```

## 2) CLAVE CANDIDATA

### Indicar la opción correcta

Dado el siguiente esquema donde se cumplen las siguientes dependencias funcionales df1 y df2:
E(a, b, c, d, e, f)

- df1) a->b, c
- df2) c->d, e

¿Cuál de las siguientes CC es la correcta?

1. CC(a,c}
2. CC(a)
3. CC(a,f) ✅
4. CC(a,c,f)
5. CC(f)

**Correcion**
```
La clave candidata correcta es la 3. CC(a,f) porque:
- con el atributo a obtengo el conjunto de atributos b y c.
- como ya obtuve el atributo c, puedo obtener el conjunto de atributos d y e.
- el atributo f va en la clave candidata porque es multivaluado, f no determina ningún atributo y no lo determina ningún atributo tampoco.
- no necesito "c" en la clave candidata porque c lo obtengo con a, no seria mínima la clave.
```
