# Redes-y-Comunicaciones-2020
# Práctica 1 - Introducción 



**1. ¿Qué es una red? ¿Cuál es el principal objetivo para construir una red?**

Una red es un grupo de computadoras/dispositivos interconectados, para que se puedan comunicar, por medio de dispositivos físicos o inalámbricos que envían y reciben impulsos eléctricos, ondas electromagnéticas o cualquier otro medio para el transporte de datos. 
El principal objetivo para construir una red es la finalidad de trabajar en conjunto, compartir información, recursos y ofrecer servicios.

**2. ¿Qué es Internet? Describa los principales componentes que permiten su funcionamiento.**

Internet es una red de redes. En realidad Internet no es una red, sino una enorme colección de distintas redes que utilizan ciertos protocolos comunes y proveen ciertos servicios comunes.Es publica global con tecnología TCP/IP.Interconecta miles de millones de dispositivos informáticos a lo largo de todo el mundo.  
Principales componentes que permiten su funcionamiento:
* Host o sistemas terminales: son todos los dispositivos que Internet interconecta. Proveen y utilizan servicios de Internet. También pueden ser clientes (computadoras con las que los usuarios se conectan a internet) que podrían estar dentro o fuera de la red.
* Red de enlaces de comunicaciones y conmutadores de paquetes: los sistemas terminales se conectan entre sí mediante esta red. 
Existen muchos tipos de enlaces de comunicaciones, los cuales están compuestos por diferentes tipos de medios físicos.  Los distintos enlaces pueden transmitir los datos a distintas velocidades.
Los conmutadores de paquetes se suministran en muchas formas y modelos, pero los dos tipos más utilizados actualmente en Internet son los routers y los switches de la capa de enlace. 
La secuencia de enlaces de comunicaciones y conmutadores de paquetes que atraviesa un paquete desde el sistema terminal emisor hasta el sistema terminal receptor, se conoce con el nombre de ruta a través de la red. Constituyen autopistas de la información
* Protocolos de red: conjunto de reglas que especifican el intercambio de datos u órdenes durante la comunicación entre las entidades que forman parte de una red. Las entidades que intercambian mensajes y llevan a cabo las acciones son los componentes hardware o software de cierto dispositivo. Los protocolos permiten la comunicación y están implementados en los componentes. Los sistemas terminales, los conmutadores de paquetes y otros dispositivos de Internet ejecutan protocolos que controlan el envío y la recepción de información dentro de Internet. 
El protocolo TCP (Transmission Control Protocol, Protocolo de control de transmisión) y el protocolo IP (Internet Protocol, Protocolo Internet) son dos de los protocolos más importantes de Internet. El protocolo IP especifica el formato de los paquetes que se envían y reciben entre los routers y los sistemas terminales. Los principales protocolos de Internet se conocen colectivamente como protocolos TCP/IP y son dos protocolos importantes para internet.


**3. ¿Qué son las RFCs?**

Las RFCs(Request For Comments, Solicitud de comentarios) son documentos asociados a los estándares IETF.
Los estándares de Internet son desarrollados por el IETF (Internet Engineering Task Force, Grupo de trabajo de ingeniería de Internet). 
Cuando se necesitaba un nuevo estándar, se discutía y si se aprobaba la comunicación se llevaba a cabo mediante la serie de informes técnicos RFC.
Los RFC nacieron como solicitudes de comentarios de carácter general para solucionar los problemas de diseño de la red y de los protocolos a los que se enfrentó el precursor de Internet [Allman 2011]. El contenido de estos documentos suele ser bastante técnico y detallado. Definen protocolos tales como TCP, IP, HTTP (para la Web) y SMTP (para el correo electrónico). Actualmente, existen más de 7.000 documentos RFC. Se guardan en línea y cualquiera que se interese en ellos puede obtenerlos en www.ietf.org/rfc. Se enumeran en orden cronológico de creación. 

**4. ¿Qué es un protocolo?**

Un protocolo define el formato, el orden de los mensajes intercambiados y las acciones que se llevan a cabo en la transmisión y/o recepción de un mensaje u otro evento. Es un acuerdo entre las partes que se comunican para establecer la forma en que se llevará a cabo esa comunicación. 

**5. ¿Por qué dos máquinas con distintos sistemas operativos pueden formar parte de una misma red?**

Porque cada máquina independientemente de su sistema operativo para comunicarse utiliza el mismo protocolo que otra máquina con diferente sistema operativo. Entonces que tengan distintos sistemas operativos no quiere decir que no puedan trabajar en conjunto para ofrecer servicios. Por lo tanto se puede formar una red con máquinas que manejan distintos sistemas operativos y cada una se encargará de “entender” y llevar a cabo correctamente los protocolos para poder comunicarse. 
Ambas máquinas implementan de diferente manera los protocolos porque son distintos S.O. Obviamente no se pueden salir del estándar de la RFC que dice que tiene que hacer porque sino “van a hablar distinto idioma” y no se van a entender. Mientras hablen el mismo idioma se van a entender, entonces, lo que importa es que respeten las funcionalidades e implementación del protocolo, el orden y el tipo de mensaje que están establecidos.
Siempre es así, por ejemplo si un sistema operativo no tiene implementado X protocolo, es cuestión de implementarlo, eventualmente puede haber una capacidad técnica que no permita a algún S.O implementar algo en particular pero sería un caso muy particular.
Por ejemplo, el arduino, que no tiene SO, o sea no tiene capacidad de cómputo suficiente para implementar el protocolo entonces esto es una limitación técnica del dispositivo. No maneja bien las encriptaciones o no es suficiente para manejar protocolos que sean encriptados pero no significa que no haya un rebusque para hacer que el dispositivo también pueda implementar. Se venden anexos de arduinos para resolver la parte de encriptación en ese anexo, así se va complejizando el dispositivo. 
En fin, si no hay limitaciones técnicas es una cuestión de implementación. 

**6. ¿Cuáles son las 2 categorías en las que pueden clasificarse a los sistemas finales o End Systems? Dé un ejemplo del rol de cada uno en alguna  aplicación distribuida que corra sobre Internet**

Los sistemas finales se pueden clasificar en dos categorías: clientes y servidores. 
De un modo informal, se puede decir que los clientes suelen ser las computadoras de escritorio y portátiles, los teléfonos inteligentes, etc., mientras que los servidores suelen ser equipos más potentes que almacenan y distribuyen páginas web, flujos de vídeo, correo electrónico, etc. 

**7. ¿Cuál es la diferencia entre una red conmutada de paquetes de una red conmutada de circuitos?**

En las redes de conmutación de circuitos, los recursos necesarios a lo largo de una ruta (buffers, velocidad de transmisión del enlace) que permiten establecer la comunicación entre los sistemas terminales están reservados durante el tiempo que dura la sesión de comunicación entre dichos sistemas terminales. 
En las redes de conmutación de paquetes, estos recursos no están reservados; los mensajes de una sesión utilizan los recursos bajo petición y, en consecuencia, pueden tener que esperar (es decir, ponerse en cola) para poder acceder a un enlace de comunicaciones. 
Agregado:
En la conmutación de circuitos los equipos de conmutación deben establecer un camino físico entre los medios de comunicación previo a la conexión entre los usuarios. Este camino permanece activo durante la comunicación entre los usuarios, liberándose al terminar la comunicación. Ejemplo: red telefónica conmutada. Su funcionamiento pasa por las siguientes etapas: solicitud, establecimiento, transferencia de datos y liberación de conexión.
En conmutación de paquetes el emisor divide los mensajes a enviar en un número arbitrario de paquetes del mismo tamaño, donde adjunta una cabecera y la dirección origen y destino así como datos de control que luego serán transmitidos por diferentes medios de conexión entre nodos temporales hasta llegar a su destino.
Cada red es independiente. Se usa una red u otra, ambas no.
Red conmutada por paquetes: el mensaje se “troza” en partes y puede tomar distintos caminos. No se desperdicia el ancho de banda.
En circuitos, como está reservado, capaz sobra espacio y se desperdicia. Difícil perder información, tiene que haber algún daño.
Pérdida de información con paquetes → lo vemos más adelante.

**8. Analice qué tipo de red es una red de telefonía y qué tipo de red es Internet.**

Una red de telefonía es una red de conmutación de circuitos. 
Internet es una red de conmutación de paquetes pública, global con tecnología TCP/IP.

**9. Describa brevemente las distintas alternativas que conoce para acceder a Internet en su hogar.**

Los sistemas terminales acceden a Internet a través de los ISP. Incluyendo los ISP residenciales, como son las compañías telefónicas o de cable locales; los ISP que proporcionan acceso inalámbrico (WiFi) y los ISP de datos móviles, que proporcionan acceso móvil a nuestros teléfonos inteligentes y otros dispositivos. Cada ISP es en sí mismo una red de conmutadores de paquetes y enlaces de comunicaciones. Los ISP proporcionan una amplia variedad de tipos de acceso a red a los sistemas terminales, entre los que se incluyen el acceso de banda ancha residencial, mediante módem por cable o DSL; el acceso LAN (Local Area Network, Red de área local) de alta velocidad y el acceso inalámbrico para dispositivos móviles.

**10. ¿Qué ventajas tiene una implementación basada en capas o niveles?**

* Divide la complejidad en componentes reusables.
* Las capas de abajo ocultan la complejidad a las de arriba, abstracción.
* Las capas de arriba utilizan servicios de las de abajo: Interfaces, similar a APIs. 
* Los cambios en una capa no deberían afectar a las demás si la interfaz se mantiene.
* Facilita el desarrollo, evolución de las componentes de red asegurando interoperabilidad. 
* Facilita el aprendizaje, diseño y administración de las redes.

**11. ¿Cómo se llama la PDU de cada una de las siguientes capas: Aplicación, Transporte, Red y Enlace?**

Pdu: unidad de datos de cada capa del protocolo. Es el nombre de la unidad en cada capa. 
* PDU de la capa de Aplicación: APDU o Datos
* PDU de la capa de Transporte: TPDU o Segmento
* PDU de la capa de Red: Paquete
* PDU de la capa de Enlace: Trama

**12. ¿Qué es la encapsulación? Si una capa realiza la encapsulación de datos, ¿qué capa del nodo receptor realizará el proceso inverso?**

Definición genérica:
Encapsulación: la idea fundamental es que una pieza particular de software (o hardware) provee un servicio a sus usuarios pero mantiene ocultos los detalles de su estado interno y los algoritmos que utiliza.

La encapsulación es el proceso que se va dando en el traspaso de capas del protocolo donde al dato se lo encapsula agregando más información en la  cabecera. Cada capa incorpora y maneja información que es de esa capa. 
Por ejemplo, tengo una aplicación que manda un dato.
Entonces tengo un dato de la capa de aplicación. Al dato de la capa de aplicación, la capa de transporte le agrega información de cabecera y se forma el segmento. La capa de red hará lo mismo, y la capa de enlace también. 
Cuando se termina, lo que se envía es la trama, que adentro tiene encapsulado todo lo que es el dato. Es como si fuera una cebolla, lo de adentro es el dato y lo de afuera que se manda, es la cebolla entera  que seria la pdu de enlace. 
Del otro lado cuando esto llega, se van “pelando o sacando” las capas, entonces se saca la capa de enlace, y se pasa al siguiente y así hasta llegar al “centro de la cebolla” que es el dato. 
No toda la información entre dos dispositivos es dato de aplicación. A veces, se envían datos desde transporte para abajo u otros ejemplos, es decir, no necesariamente todos los mensajes incluyen todas las capas. Si de abajo para arriba, ese orden está casi siempre. Primero está encapsulado en la capa de enlace, luego en red, luego en transporte y por último en aplicación pero por ejemplo, puede llegar solamente hasta red o solamente hasta enlace y ser mensajes que se envían así y llegan solo a la capa receptora de la misma que se envió.
O sea si solo se envio de red, se le agrega información de enlace, y en la capa receptora solo se llegara hasta red.

Encapsulación: es el proceso que se produce de ir pasando la información a la capa correspondiente y que cada capa le va agregando las cabeceras que corresponden a esa capa.
Si una capa realiza la encapsulación de datos, ¿qué capa del nodo receptor realizará el proceso inverso?
Cada capa va “pelando” lo que le corresponde y pasando a la siguiente. O sea, cada capa va tomando los datos que le corresponden, los interpreta y envía a la capa superior, porque estamos en el receptor y esta desencapsulando, o sea haciendo el proceso inverso y entonces, mira los datos correspondientes a la capa anterior y los envía a la capa superior.
Dicho de otra manera, si una capa X realiza el encapsulamiento en el nodo emisor, la misma capa X será la encargada de hacer el proceso inverso en el nodo receptor.-

**13. Describa cuáles son las funciones de cada una de las capas del stack TCP/IP o protocolo de Internet.**

Modelo de 4 capas: 
* Capa de Aplicación (Process/Application): 
* Capa de Transporte o Host-to-Host
* Capa de Internet o Internetworking 
* Capa de Acceso a la red (NAL)

Función de capa de aplicación:
* Provee servicios de comunicación a los usuarios y a las aplicaciones, incluye las aplicaciones mismas.
* Existe un modelo de comunicación Machine to machine (M2M), no hay usuarios (personas). 
* Interfaz con el usuario -User Interface (UI)- u otras aplicaciones/servicios. 
* Las aplicaciones que usan la red pertenecen a esta capa. Los protocolos que implementan las aplicaciones tambien.
* Existen aplicaciones que NO son de red que deben trabajar con aplicaciones/servicios para lograr acceso a la red.

Función de capa de transporte:
* Está diseñada para permitir que las entidades pares, en los nodos de origen y de destino, lleven a cabo una conversación
* Transporta los mensajes de la capa de aplicación entre los puntos terminales de la aplicación. 
* Existen dos protocolos de transporte:  TCP y UDP, pudiendo cada uno de ellos transportar los mensajes de la capa de aplicación.
* TCP ofrece a sus aplicaciones un servicio orientado a la conexión. 
* UDP proporciona a sus aplicaciones un servicio sin conexión. 
* El mensaje de la capa de aplicación y la información de cabecera de la capa de transporte constituyen el segmento de la capa de transporte. El segmento de la capa de transporte encapsula, por lo tanto, el mensaje de la capa de aplicación. 

Función de capa de Internet:
* Es responsable de trasladar los paquetes de la capa de red, conocidos como datagramas, de un host a otro.
* Incluye el conocido protocolo IP, que define los campos del datagrama, así como la forma en que actúan los sistemas terminales y los routers sobre estos campos. 
* También contiene protocolos de enrutamiento, que determinan las rutas que los datagramas siguen entre los orígenes y los destinos. 

Función de capa de Acceso a la red: 
* Esta describe qué enlaces se deben llevar a cabo para cumplir con las necesidades de esta capa de interred sin conexión. En realidad es como si fuera una interfaz entre los hosts y los enlaces de transmisión.
* Un datagrama puede ser manipulado por distintos protocolos de esta capa en los distintos enlaces disponibles a lo largo de la ruta. 
* Mover tramas completas de un elemento de la red hasta el elemento de red adyacente
* Mover de un nodo al siguiente los bits individuales que forman la trama. (capa física)
* Los protocolos son dependientes del enlace y, por lo tanto, dependen del medio de transmisión del enlace.  En cada caso, los bits se desplazan a través del enlace de forma diferente.

**14. Compare el modelo OSI con la implementación TCP/IP**

_Similitudes:_
* Ambos modelos se basan en el concepto de una pila de protocolos independientes. 
* La funcionalidad de las capas es muy similar. 
* Las capas que están arriba de la de transporte son usuarias orientadas a la aplicación del servicio de transporte.
* Ambos tienen capas de (inter)red, transporte y aplicación

_Diferencias:_
* Los protocolos en el modelo OSI están ocultos de una mejor forma que en el modelo TCP/IP, además se pueden reemplazar con relativa facilidad a medida que la tecnología cambia.
* El modelo de referencia OSI se ideó antes de que se inventaran los protocolos correspondientes. Este orden significa que el modelo no estaba orientado hacia un conjunto específico de protocolos, un hecho que lo hizo bastante general.
* La desventaja de este orden fue que los diseñadores no tenían mucha experiencia con el tema y no supieron bien qué funcionalidad debían colocar en cada una de las capas. 
* Con TCP/IP sucedió lo contrario: primero llegaron los protocolos y el modelo era en realidad sólo una descripción de los protocolos existentes. No hubo problema para que los protocolos se ajustaran al modelo. 
* Número de capas: el modelo OSI tiene siete capas, mientras que el modelo TCP/ IP tiene cuatro.
* Hay otra diferencia en el área de la comunicación sin conexión frente a la comunicación orientada a conexión. El modelo OSI soporta ambos tipos de comunicación en la capa de red, pero sólo la comunicación orientada a conexión en la capa de transporte, en donde es más importante (ya que el servicio de transporte es visible a los usuarios). El modelo TCP/IP sólo soporta un modo en la capa de red (sin conexión) pero soporta ambos en la capa de transporte, de manera que los usuarios tienen una alternativa, que es muy importante para los protocolos simples de petición-respuesta.
