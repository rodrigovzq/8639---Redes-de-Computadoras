
# Preguntas de Introducción, LAN, LAN Switching, STP, VLANs

## Introducción

- ¿Comprende la necesidad de utilizar sistemas intermediarios (IS) para interconectar en red a los sistemas extremos (ES)?

- ¿Comprende los conceptos de conmutacion y multiplexado? ¿Conoce los distintos tipos de conmutacion y multiplexado posibles?


- ¿Que tipo de conmutacion y multiplexado se usa en las redes Ethernet/IP?
	- Multiplexado
		- FDM
			- no asegura ancho de banda
			- aprovecha BW
		- TDM
			- estadistico STDM
			- asegura ancho de banda
			- desperdicia BW
		- DWDM: Dense wavelength 
			- se usa en fibra optica
	- Conmutacion
		- Paquet switching
			- aprovecha mejor los recursos disponibles
			- recursos mas baratos
			- no garantiza BW ni delauy
- ¿Que diferencias hay entre las tecnologias LAN y WAN? ¿Cual es el "cost driver" de cada una de ellas?
	- cost-driver es el limitante para que el producto se desarrolle
	- WAN
		- **cost driver: ancho de banda**
		- headers chicos
		- procotolos orientados a la conexion
			- minizan headers
			- FRAME RELAY
			- ATM
	- LAN
		- **cost driver: costo de conexion por boca de red**
		- maximizar cantidad de conexiones
		- minimizar costo de conexion
		- bufferizacion en switching
			- alojar colas
			- tener suficiente memoria

- ¿Conoce la terminologia y conceptos asociados a una red de arquitectura basada en capas?

- Defina los conceptos de entidad, funcion, protocolo, encapsulamiento, interfaz de servicio.

- ¿Que define un modelo en capas? ¿Que define una arquitectura de red?

- ¿Conoce el modelo de referencia OSI y puede explicar las funciones de cada capa?

- ¿Conoce el modelo en capas TCP/IP?  Compare las funciones de cada capa con el modelo de referencia OSI.

- ¿Podría asignar protocolos a cada capa del modelo TCP/IP?

- ¿Cuales son las funciones principales de IP?

- ¿Qué diferencias hay entre repeater/hub, lan switch, router, proxy/gateway? ¿A qué nivel de red funcionan estos ISs?

- ¿Qué significa S&F? ¿Qué pros y contras presenta? ¿Qué ISs usan S&F? 




## LAN Ethernet
- ¿Como se hace en Ethernet para sincronizar la recepcion y deteccion digital en los recepctores con el transmisor?

- ¿Qué problemas ocurren cuando todas las estaciones envían y reciben a través de un medio?

- ¿Cómo funciona la detección de colisiones? ¿En que se basa?

- ¿Qué es “Carrier Sense Multiple Access/ Collision Detection” (CSMA/CD) y cómo funciona?

- ¿Qué es el retroceso exponencial binario truncado y qué problema resuelve?

- ¿Cómo se estructura una trama Ethernet (Ethernet II, IEEE 802.3/802.2)?

- ¿Cómo se estructura una dirección MAC?

- ¿Cuáles son las topologías comunes de Ethernet? Diferencie topologia de capa PHY de topologia de capa MAC.

- ¿Cómo funciona la detección de errores con redundancia en la transmisión de datos Ethernet?

- ¿Cuál es la diferencia entre un dominio de colisión y un dominio de broadcast?

- ¿Cual es el mecanismo utilizado en un IS para separar dominios de colision?



- LAN Switching
- ¿Cuáles son las principales funciones implementadas en las entidades Transparent Bridging o LAN Switching?

- ¿Cómo funciona el mecanismo de filtrado?

- ¿Qué hace el LAN Switch con los Broadcasts y los Unknown Frames?

- ¿Cómo se realiza el aprendizaje (learning) de direcciones MAC?

## STP

- ¿Qué puede pasar en una topología con caminos redundantes?

- ¿Qué se debe hacer en una topología con rutas redundantes para evitar bucles?

- ¿Qué significa STP?

- ¿Cómo funciona STP?

- ¿Qué significa BPDU?

- ¿Qué campos tiene el encabezado de una BPDU?

- ¿En qué PDU está encapsulada una BPDU?



## VLANs
- ¿Qué es una VLAN?

- ¿Cuáles son las ventajas de las VLAN?

- ¿Cómo se puede configurar una VLAN? ¡Mencione al menos tres criterios!

- ¿Donde y por qué se necesita el etiquetado de tramas o VLAN trunking?

- ¿Cómo funciona el VLAN trunking?