# Preguntas de IP, ARP, ICMP



## IP

- ¿Cuales son las 3 funciones principales de IPv4?

>	1. [[Unidad I - Repaso - COM#Preguntas|Interconexion de redes heterogeneas]]
>	2. Identificacion de la interfaz de red
>	3. Direccionamiento para su ubicacion

- ¿Que significa el campo IHL del datagrama IPv4? ¿Cual es la longitud minima y maxima del header IPv4?

- ¿Cual es el campo del datagrama IPv4 que limita la longitud del datagrama IPv4? ¿Cual es la longitud maxima del datagrama IPv4?
> Total Length (TL): Especifica el largo total del datagrama IP expresado en bytes. Como el campo es de 16bit de ancho, el largo maximo de un datagrama IP es $2^{16} = 65535$ bytes = 64kB. Pero hay que restar el header. El record route no se usa porque no se tuvo en cuenta que el header iba a ocupar lugar entonces mas de 9 direcciones no entran. Por eso se inventa el traceroute

- ¿Para que sirve el campo "Protocol" del header IPv4?
> Identifica el procolo de la capa superior (capa de transporte normalmente) donde es transportado el datagrama.
> ![[Pasted image 20230320152951.png]]


- ¿Para que sirve el campo TTL?
>  Time To Live: especifica por cuantos saltos tiene permitido vivir un datagrama. Cada router decrementa este campo previo a transmitirlo.

- ¿Para que se usa el campo TOS? ¿Que otra sigla/nombre se le ha dado?
> Type of Service: Contiene la informacion de calidad de servicio disponible, como entrega priorizada. Nunca se uso mucho. 
> Otro nombre es QoS?

- ¿Cual es la longitud minima del header IPv4?
> 21 bytes = 20 del encabezado y 1 de data

- ¿Cual es la longitud maxima de un datagrama IPv4?
> 65535 bytes

- ¿Cuales son los campos del header IPv4 que cambian en cada salto? ¿Cuales son los que por lo general no cambian?
> Cambian en cada salto:
> 	TTL
> 	Flags
> 		Fragmentation
> 	Fragment offset
> 	Checksum
> No cambian:
> 	Source Address
> 		Cambia si pasan por una entidad de NAT. Cuando sale
> 	Destination Adddress
> 		Si cambia si pasan por una direccion NATeada. Cuando entra
> 	ToS
> 	Procotol
> 	Identification

## Direccionamiento IP

- ¿Para que se asigna una mascara, ademas de una direccion IP, a cada interfase IP?
> Para saber la red a la que pertence, haciendo IP^Mascara=Red. Simplificar el ruteo, agrupando hosts

- ¿Que diferencia conceptual tienen la mascara de una interfase con la mascara de una ruta CIDR?
> Mascara asociada a la ruta. detino^mascaraRuta=direccion destino -> matchea la ruta. Cualquier destino matchea la ruta default (0.0.0.0)
> Mascara de interfase es IP^mascara=red

- ¿Que notacion se suele usar para representar las direcciones IPv4? ¿Y para representar las mascaras?
> Decimal Dotted Notation (DDN): ---.---.---.--- se usa en mascara e ip.
> Notacion de prefijo \n se usa para mascaras. n siendo la cantidad ed bits en 1.

- En base a la direccion IP y mascara de una interfase, ¿como se obtiene la direccion de red y la direccion de broadcast de la subred a la que esta conectada?
> broadcast = IP+ not(mascara)
> IP red = IP ^ mascara

- ¿Para qué se divide al espacio de direccionamiento en clases?
> Classfull routing no habia mascaras, para saber la ip de la red habia que aplicar mascara default.
> 	A -> /8
> 	B -> /16
> 	C -> /24
> En classfull routing se puede hacer subnetting pero la longitud de la mascara es fija. Por eso solo se peude hacer fixed length subnetting
> En Classless es mas sencillo, porque cada uno tiene su mascara. Dada la direccion destino, se hace `and` con la mascara y se encuentra asi la direccion destino.
> **Para poder utilizar de manera racional cada espacio de clasificacion**

- Para las clases A, B y C, ¿como identifica la clase en funcion del octeto mas significativo? 
> A: 0-127, net#: `xxx`
> B: 128-191, net#: `xxx.xxx`
> C: 192-223, net#: `xxx.xxx.xxx`
> D: 224-239, se usa para `multicast`
> E: 240-255 -> no se usa

- Para las clases A, B y C, ¿cuales son los octetos que definen el netnumber?
> A: Primero mas significativo
> B: Primeros dos mas significativos
> C: Primeros tres mas significativos> 

- ¿Para qué se hace subnetting? 
> Para aprovechar mejor el espacio de direcciones

- En base a la direccion IP y mascara de una interfase ¿Cuando se hace subnetting? ¿Cual es la mascara default para cada clase?
> Clase A: 255.0.0.0 -> /8
> Clase B: 255.255.0.0 -> /16
> Clase C: 255.255.255.0 -> /24
> Se hace subnetting es usar en una interfaz una mascara de mayor longitud que la dada por la default de la clase

- En base a las direcciones IP y mascaras de interfases de una red y subredes ¿Cuando se hace subnetting de longitud de mascara fija FLSM y cuando se hace subnetting de longitud de mascara variable VLSM?
> Se usa FLSM cuando se agrupa hosts en grupos que tengan la misma cantidad de hosts, es decir, se tiene una unica mascara para todos y VLSM (solo soportado en Classless) cuando se necesite agrupar con una cantidad diferente de hosts entre grupos.
> FLSM es direccionamiento y VLSM es ruteo

- ¿Qué beneficio aporta el VLSM respecto del FLSM?
> **Mayor graunlaridad**, mas capacidad de crecimiento,

- ¿Cual es la direccion llamada localhost? ¿Para que se usa?
> `127.0.0.0` Es la direccion de loopback de un hosts. Enviarse datos a si misma y no genera trafico en la red fisica.

- ¿Para qué se usa la clase D? ¿En que consiste y para que sirve el direccionamiento multicast?
> Sirve para identificar a un grupo de hosts que no sean una red. `224.0.0.1` es la direccion a la cual escucha IGMP. Es el que descubre grupos en las cercanias.
> El direccionamiento multicast permite enviar datos a un grupo de dispositivos en lugar de a un solo dispositivo.



## Ruteo IP

- ¿En que se basa el ruteo IP? ¿Que significa DABR?
> El enrutamiento IP se basa en la idea de que cada dispositivo en una red tiene una dirección IP única y que los paquetes de datos se envían de un dispositivo a otro a través de una serie de dispositivos intermedios llamados routers. Los routers utilizan información de enrutamiento para determinar la mejor ruta para enviar paquetes de datos de una red a otra.
> En DABR, cada router mantiene una tabla de enrutamiento que contiene información sobre las direcciones de destino de los paquetes y la interfaz de salida correspondiente para enviarlos. Cada vez que un paquete llega a un router, se utiliza la dirección de destino del paquete para buscar en la tabla de enrutamiento y determinar la interfaz de salida adecuada. Si no se encuentra una entrada en la tabla de enrutamiento para la dirección de destino del paquete, el paquete se envía a través de una interfaz predeterminada o se descarta si no hay una interfaz predeterminada configurada

- ¿Cuales son los campos de una tabla de ruteo?
> Next 
[![CCNA CISCO: VISUALIZACIÓN DE TABLAS DE ENRUTAMIENTO DE HOST](https://3.bp.blogspot.com/-fH_kk3h29nw/VcS1rSTJJgI/AAAAAAAAAUE/gtO2Bglt2ic/s1600/lab%2B6b.png)

- ¿Cuales son los campos de la tabla de ruteo que se utilizan para indicar por donde forwardear el datagrama?
> la dirección de red de destino, la máscara de subred, la dirección del siguiente salto (o interfaz de salida), la métrica y la interfaz de entrada.

- Con solo ver los campos de una tabla de ruteo, ¿Como se puede saber que el ruteo es classful o classless?
> Si hay campo mascara, es classless. Si fuera classfull, no habria campo mascara porque seria una sola

- ¿Cuales son los beneficios de usar una mascara de ruta?
> Se puede hacer summarizacion de rutas(supernetting) ,simplifica la tabla de ruteo. Usar mascara implica usar classless que implica poder usar VLSM por lo tanto hay **mas granularidad** en el uso de direcciones.

- ¿Cuales son los campos de la tabla de ruteo CIDR que se utilizan para seleccionar la mejor ruta?
> Primero la mascara, despues la metrica.
> CIDR: Classless internet domain routing

- ¿Como se hace el "matcheo" de la ruta en base a la direccion destino?
> Dada la direccion destino y se chequea que `HostAdd ^ RouteMask == DestAdd`. En caso de que ambos coincidan, se usa la mascara mas larga

- ¿En que orden se escruta la tabla de ruteo?
> Mascara de mas larga a mas corta

- ¿Si la direccion destino del datagrama matchea 2 o mas rutas con diferente longitud de mascara, cual de ellas se usa?
> La mas larga

- ¿Si la direccion destino del datagrama matchea 2 o mas rutas con igual longitud de mascara, cual de ellas se usa?
> La de menor metrica

- En los routers Cisco ¿que diferencia conceptual hay entre la distancia administrativa y la metrica de una ruta?
> La distancia administrativa se utiliza para **seleccionar entre diferentes** *fuentes de información* de rutas para la misma red de destino, mientras que la métrica se utiliza para seleccionar la *mejor ruta* hacia una red de destino específica en la tabla de enrutamiento.
- ¿Porque un host IP (con 1 sola interfase) necesita una tabla de ruteo?
> Para alcanzar otras ip (direccionamiento indirecto), pasar por la default gateway.
> Para diferenciar de localhost

- ¿Que hace el router con un datagrama si su direccion destino "no matchea" ninguna ruta?
> Descarta el datagrama y envia un mensaje de "destino inalcanzable" (ICMP) al origen del datagrama

- ¿Como es la ruta default en CIDR? ¿Porque "matchea" cualquier direccion destino?
> ruta =`0.0.0.0` y con mascara `0.0.0.0` entonces al hacer `and` con cualquier direccion de destino, da la ruta default.

- ¿Que diferencia hay entre una ruta directa y una ruta indirecta?
> la primera se refiere a una red conectada directamente al router, mientras que la segunda se refiere a una red que no está directamente conectada al router y requiere que el tráfico pase a través de otros dispositivos de red para llegar a su destino.
> La ruta directa es la que no tiene next hop, y en windows es cuando en la tabla de ruteo dice `On Link`. Y generalmente la metrica es 0

- ¿Cuales son las diferencias conceptuales entre el direccionamiento MAC y el direccionamiento IP?
> es que el primero se refiere a una dirección física única asignada a un dispositivo de red por su fabricante, mientras que el segundo se refiere a una dirección lógica asignada a un dispositivo conectado a una red IP. En IP hay informacion topologica/geolocalizada, se adminte ruteo.
> El direcc MAC esta vinculador al switching (no rutea, elige el mejor camino que el spanning tree le permite usar) y el direccionamiento IP esta vinculado al ruteo (elige el mejor camino siedo este el mas corto)
- ¿Porque el ruteo classful no soporta VLSM? 
> Porque utiliza una unica mascara de red para todos los hosts. La mascara sale de una funcion f(netnumber)=mascara. Si no hay una mascara especificada, se usa la default.
- ¿En que consiste el supernetting o agregacion/sumarizacion de rutas? Cual es el beneficio que aporta?
> El proceso que combina varias redes adyacentes en una sola. Se logra mediante el uso de mascaras.
> Se reduce el numero de la mascara y se conserva el next hop. Los routers hacen autosummary
> Ventaja: Mayor eficiencia en el uso del espacio de direcciones IP y reduccion en la carga de procesamiento de los routers. Se reduce la cantidad de filas en la tabla de ruteo
> Solo puede hacer el CIDR

- ¿Porque el ruteo classful no soporta supernetting?
> porque en el ruteo classful, la longitud de la máscara de subred se determina automáticamente en función de la dirección IP y la clase de la red a la que pertenece. Por lo tanto, no hay manera de especificar una máscara de subred personalizada para una red específica, lo que es necesario para el supernetting.



## Fragmentacion IP 

- ¿Por qué/para qué IP implementa una funcion de fragmentacion?
> Cuando los datos a enviar superan el tamaño maximo que se puede empaquetar en un datagrama. Este tamaño maximo depende de cada red (MTU). Si no se puede fragmentar, se descarta

- ¿Qué entidades fragmentan en IPv4? (y en IPv6?) ¿Qué entidad reensambla?
> Fragmentan en ipv4-> hostOrigen y routers
> Fragmentan en ipv6 -> hostOrigen
> Reensamblan -> hostDestino

- ¿Cuales son los campos del header IPv4 que se usan en la fragmentacion?
> ID: identificar de manera unica cada fragmento de datos
> Fragmentation Flag:
> 	DF: Dont fragment
> 	MF: More fragments. En 1 si hay mas fragmentos del actual
> Fragmentation offset: se utiliza para indicar la posicion de cada fragmento en relacion al inicio del paquete original

- ¿Como se identifica al primer fragmento? ¿Y al ultimo?
> Primero MF=1 y Ultimo MF=0

- ¿Como se identifica a un datagrama que no fue fragmentado?
> MF =0 y FO = 0

- ¿Que sucede si un fragmento no llega al destino?
> Hay un timeout

- ¿En que fragmento viaja el header de TCP/UDP/ICMP?
> En el primero

- ¿Porque la longitud de los primeros fragmentos debe ser multiplo de 8 bytes?
> Porque el FO esta codificado en 13 bits y 3 usados para flags, 2³=8, entonces la identificacion de los fragmentos son multiplos de 8



## ARP

- ¿Para qué sirve el protocolo ARP?
> Address Resolution Protocol se utiliza para resolver direcciones fisicas (MAC) de una direccion logica (IP) en una **red local**.
> En una red remota, obtengo la MAC del defaul gateway, no la del dispositivo. Se hace un arpreq del next hop del router

- ¿En que protocolo se encapsula el mensaje ARP?
> en un paquete Ethernet. El encabezado contiene la direccion fisica del emisor y repector, mientras que el mensaje ARP  contiene las direcciones logicas del emisor y repecitopr junto con la MAC del emisor

- ¿Que direcciones MAC e IP contiene el ARP Request? ¿Y el ARP Reply?
> ARP REQ: IP del dispositivo que se esta buscando y la MAC del que envia la solicitud
> ARP REPLY: MAC del dispositivo que se esta buscando y su IP

- ¿A que direccion MAC destino va dirigida la trama Ethernet que contiene el ARP Request? ¿Y el ARP Reply?
> La trama ARP REQ va dirigida a la direccion broadcast y el ARP Reply va dirigida a la direccion MAC del dispositivo que envio la solicitud. 

- ¿Para que se usa el ARP cache? 
> Es una tabla de buscqueda que se utiliza para almacenar temporalmente las direcciones MAC de dispositivos en una Red local.
- ¿Cuanto tiempo suele durar cada registro en el ARP cache? 
> Depende de la configuracion, puede ir de algunos minutos o algunas horas. default 20 min

- ¿Que sucede si la direccion destino no figura en el ARP Cache?
> El emisor envia una solicitud ARP broadcast a todos los dispositivos de la red, solicitando la direccion fisica del dispositivo destino. La respuesta se almacena en el cache.

- ¿Puede haber entradas estaticas en el ARP Cache? ¿Para qué pueden servir?
> Si, se insertan manualmente y pueden servir para asignar una ip a una mac? evitar ataques de arp poisoning?
> Evitar una falsa arp reply

- ¿Qué sucede si no se obtiene respuesta a un ARP Request?
> significa que el destino no esta presente en la red. Aunque puede ser por un error de conectividad o de configuracion



## ICMP

- ¿Cual es la funcion de ICMP?
> Internet Control Message Protocol es un protocolo de capa de red que se usa para enviar mensajes de control y error entre dispositivos en una red IP (protocol 1). Proporciona informacion sobre errores y problemas de red.
> Herramienta Ping

- ¿En que protocolo se encapsula el mensaje ICMP?
> Se encapsulan en paquetes IP, con IPorigen e IPdestino
> Type, code, checksum

- ¿Que campos de informacion tiene el mensaje ICMP?
> Tipo de mensaje: un número que indica el tipo de mensaje ICMP, como un mensaje de solicitud de eco (ping) o un mensaje de error de destino inalcanzable.
> Código: un número que proporciona información adicional sobre el tipo de mensaje ICMP. Por ejemplo, en un mensaje de error de destino inalcanzable, el código indica el tipo de error.
> Checksum: un valor que se utiliza para garantizar la integridad del mensaje ICMP y para detectar errores en la transmisión.
> Identificador y número de secuencia: utilizados en algunos tipos de mensajes ICMP para ayudar a identificar el mensaje específico y su orden.

- ¿Como funciona el comando "ping"? ¿Para que sirve? ¿Que mensajes ICMP son usados en el "ping"?
> Se utiliza para validar conectividad.
> **Mensajes de solicitud de eco** (tipo 8, código 0): se utilizan para enviar los paquetes de solicitud de eco al dispositivo de destino. Estos paquetes contienen información que se utiliza para identificar el mensaje y para enviar datos de prueba al dispositivo de destino.
> **Mensajes de respuesta de eco** (tipo 0, código 0): se utilizan para responder a los paquetes de solicitud de eco recibidos. Estos paquetes contienen los mismos datos de prueba que se enviaron en el paquete de solicitud de eco y se utilizan para verificar la conectividad y medir la latencia entre los dispositivos.

- ¿Qué mensaje ICMP es enviado al source host del datagrama si su direccion destino no matchea ninguna ruta?
> Devuelve el mensaje *destino inalcanzable*

- ¿Qué mensaje ICMP es enviado al source host del datagrama si, en la ruta directa final al host destino,el router no obtiene respuesta al ARP request?
> *Destino inalcanzable*

- ¿Qué mensaje ICMP es enviado al source host del datagrama si se agota el TTL?
> *Time Exceeded*

- ¿Como funciona el comando "traceroute/tracert"? ¿Para que sirve? ¿Que mensajes ICMP son usados en el "traceroute/tracert"?
> Se usa para rastrear la ruta que toma un paquete de red. Funciona con una serie de paquetes ICMP con incrementos graduales en el TTL. Cada vez que alcanza un router, el TTL se decrementa, cuando llega a 0 se envia un *Time exceeded* y el traceroute muestra ese tiempo de respuesta junto con la ip que lo envio, asi armando una ruta de los hop involucrados en el camino entre el origen y destino.

- ¿Qué mensaje ICMP es enviado al source host del datagrama si se pierde un fragmento?
> *time exceeded*, codigo 1

## IPv4 NAT

- ¿Cuales son las direcciones IPv4 que se pueden usar en una red privada?
> clase A, B y C
> ![[Pasted image 20230403184129.png]]
> 

- ¿Qué entiende por NAT? ¿Para que sirve?
> Network Address Translation es un protocolo para traducri ip privadas en ip publicas. Se utiliza normalmente en los routers de la red para permitir que los dispositivos de la red privada accedan a internet usando una sola IP publica.

- ¿Como se relaciona el NAT con el Control Perimetral?
> Se utiliza NAT en control perimetral. Este es un conjunto de medidas de seguridad en la frontera de una red privada.
> Se utiliza NAT en firewalls, routers y dispositivos de seguridad de red 

- ¿En que dispositivo de red se suele implementar el proceso de NAT?
> routers y firewalls

- Cuando un datagram IP egresa de una red privada, ¿qué direccion es traducida por la entidad de NAT?
> la source

- Cuando un datagram IP ingresa a una red privada, ¿qué direccion es traducida por la entidad de NAT?
> la publica

 ¿Que entiende por one to one mapping? ¿En que caso tipicamente se aplica?

- ¿Que entiende por many to one mapping? ¿En que caso tipicamente se aplica?

- ¿Que entiende por NAPT? ¿Para que sirve? ¿En que se diferencia del NAT?
> Es un mecanismo que se produce en un equipo (Network address port translation), se realiza. NAT es un protocolo que sucede en el router o firewalls, permite que los mensajes de la red privada pasen a la interneta y viceversa