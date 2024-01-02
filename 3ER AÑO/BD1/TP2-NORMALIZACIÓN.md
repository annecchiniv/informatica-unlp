# Parte 1

**Para los esquemas propuestos en cada ejercicio aplicar y explicar el proceso de normalización visto en la teoría. Todos los esquemas ya se encuentran en 1FN.**

## 1. MAPAS PUBLICADOS
## 1) Indicar la opción correcta

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
- El esquema tiene más de una clave candidata **V**

Correcion: esta bien la que elegi, la justificacion es que tengo mas de una forma de identificar el sitio web, por idSitioWeb o dominioSitioWeb  


