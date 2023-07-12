## Temas
- LAN
- WAN
- Bridging
- LAN Switching
---

# Introduccion

- Videos en youtube
	- hay una lista de obligatorios en el campus
	- 


## Preguntas campus

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
- Costdriver de WAN y LAN
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
- Diferencia entre arquitectura y modelo
	- Capas OSI y las otras
	- una es 7 y la otra 4
- Tunel: encapsular un protocolo de capa N en un protocolo de capa N+1
- Principales funciones de ip
	- direccionamiento: 
		- a quien entregarselo
		- colabora con el ruteo -> minimizar saltos para soportar el direccionamiento
	- fragmentacion y reensamblado: MTU 
	- ruteo 
		- tabla de ruteo de longitud razonable para escalar solucion
	- implementa mecanismos
		- queue
- VLSM 
	- solo se puede con ruteo classless
- Diferencias entre repeater/hub, switch, router, proxy/gateway
	- repeater/hub 
		- es capa 1 OSI
		- tiene poco retardo
		- no hace store and forwar
		- puede hacer adaptacion de medios
		- no puede adaptar velocidades 
		- ni prevenir colisiones
			- desaprovecha ancho del canal
	- switch o bridge 
		- es capa 2
		- usa store and forward
			- evita colisiones
			- adapta velocidades
			- tiene colas (buffering) -> puede esperar
			- aprovecha mejor ancho de banda -> sirve si el BW es cost driver
		- redundancia genera loops
			- SPTP: spanning tree
				- desaprovecha recursos de comunicacion
		- 
	- router 
		- es capa 3
		- usa store and forward
		- aprovecha mejor recursos porque utiliza todos los enlaces a pesar de la redundancia
			- usa el mejor camino
	- proxy 
		- es capa 7: aplicacion
		- menos eficiente, mas lento
		- por temas de seguridad es beneficioso
			- control con mas granularidad
			- inhabilitar forwarding en capas inferiores -> aplicar tecnicas de firewalling
	- LAN switch
		- 
- Que significa S&F
	- **Store and forward**
	- repeater puede tener un retardo de 1bit
	- ruteo puede tener 10kb
	- PRO
		- evita colisiones
		- adapta velocidades
		- permite inspeccionar tramas
- Direcciones MAC
	- 48 bit
	- bits mas significativos identifican el vendor
	- bits menos sign identifican el host
### LAN switching

- Principales funciones
	- evitar colisiones
	- filtering: para que el trafico local no se retransmita en WAN
	- learning: solo forwardea si sabe que el destino esta del otro lado
		- del broadcast se guarda la MAC address del que envio
### VLAN

- redes virtuales
- se usa un switch y se separan las redes
- Motivos de seguridad
	- filtrado
	- firewall
- proveedores y datacenters proveedores de nube usan VLAN por cliente
- Hay motivos de performances porque podes separar los traficos de broadcast
	- aunque este trafico suele ser bajo comparado con los demas
- VLAN tranquing(? -> tag entre VLANs
- VLAN dentro de VLAN por limite de 4000
- 


## Protocolos orientados a la conexion

El tratamiento de un mensaje que recibe, depende del estado de un mensaje anterior, el protocolo es orientado a la conexion
Ejemplo:
**Kiosko:** el kioskero no pregunta nada previo
**Banco**: si queres plata, te hace preguntas previas. El numero de cuenta es la conexion logica, te puede dar plata porque hubo una conexion previa.


### Tabla de ruteo

```
$> route print
$> netstat -r
```
### PING
Cuando hago ping a de un host local  aun destino remoto, no se hace ARP REQ de la ip destino en elm router sino que el router hace ARP request del next hop
Se hace ARP Req y si no match de tabla local, se va el REQ a la default gateway.
Los routers por default no forwardean una trama por la misma interfaz que le llego el mensaje


---
