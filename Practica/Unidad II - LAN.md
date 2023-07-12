
# LAN & LAN Switching
23-3

Codificacion manchester (?) 10bas2

- Como se detecta una colision?
	- como la señal Ethernet es una alterna de promedio 0, cuando hay colision existe alta probabilidad de que el promedio no sea 0
	- Esto se llama Carrier Sense Multiple Addres Colission Detection
	- CSMS/CD
	- CSMA/CA: es Collision avoidance, esto es en WiFi
- Diferencia entre dominio de colision y dominio de broadcast?
	- El dominio de colision son las que comparten el medio
		- Un switch previene una colision porque levanta la trama incompleta y la descarta. (anteultima pregunta de LAN)
		- Detecta la integridad de la trama antes de hacer forwarding (store and forwarding)
	- El dominio de broadcast son las que comparten la red. Las que recibirian un mensaje si alguno envia a la direccion de broadcast
- Diferencia entre Hub vs Bus
	- Si se corta una parte del bus, se cae la red
- En los uplinks hay muchas macAddr
- Cuando un switch recive una trama broadcast, la repite por todos los puertos menos en el de entrada -> simula Bus

# VLAN
- Es como una LAN que esta definida dentro de otra LAN
- Define varios switch dentro de un switch
- Tengo tantos dominios de broadcast como VLANs
- Se crean por motivos de 
	- seguridad
	- separacion de aplicacion / grupo de trabajo
	- mucho trafico de broadcast desperdicia BW
	- menor costo que comprar varios switches 
- VLAN trunk -> lleva trafico de varios hosts en el mismo puerto sin que se pisen los dominios de broadcast
	- trama tipica de ethernet pero extendida con un tag (802.1q)

# Spanning Tree Protocol (STP)

- Protocolo abierto
- objetivo: 
	- Evitar loops
	- proveer caminos redundantes
- algunos puertos entran en blocking state y otros en forwarding state
- transforma una topologia mallada en un arbol
- Roles
	- Designated port
	- root port
- link aggregation
	- tiene redundancia y velocidad
	- 
## Comentarios de preguntas U II

- Ethernet tiene MTU tipico de 1500

---
30-3
![[Pasted image 20230330171351.png]]
# ARP

- es la forma de encontrar una direccion fisica en base a una direccion logica

![[Pasted image 20230330171511.png]]

### como es la trama en cada tramo del mensaje de A a B?

#### Trama Ethernet
[![Representación de una estructura de trama Ethernet II](https://www.ionos.mx/digitalguide/fileadmin/DigitalGuide/Screenshots_2018/EN-ethernet-frame-structure.jpg "Representación de una estructura de trama Ethernet II")](https://www.ionos.mx/digitalguide/fileadmin/DigitalGuide/Screenshots_2018/EN-ethernet-frame-structure.jpg)

## Si los dispositivos fueran switches -> capa 2
#### Tramo1
- DstMacAddr: MAC B
- SrcMacAddr: MAC A
- Type / Length: X
- Payload -> Data: ...
- CRC: X

#### Tramo2
- DstMacAddr: MAC B
- SrcMacAddr: MAC A
- Type / Length: X
- Payload -> Data: ...
- CRC: X

#### Tramo3
- DstMacAddr: MAC B
- SrcMacAddr: MAC A
- Type / Length: X
- Payload -> Data: ...
- CRC: X

## Si los dispositivos fueran routers -> capa 3
#### Tramo1
- DstMacAddr: MAC R1p1
- SrcMacAddr: MAC A
- IP: 0x0800
- Payload -> Data:
	- IP src: IP A
	- IP dest: IP B
	- TTL: 64 (ejemplo)
	- checksum: valor_tramo1

#### Tramo2
- DstMacAddr: **MAC R2p2**
- SrcMacAddr: **MAC R1p2**
- IP: 0x0800
- Payload -> Data:
	- IP src: IP A
	- IP dest: IP B
	- TTL: **63** 
	- checksum: *valor tramo2*
- CRC: X

#### Tramo3
- DstMacAddr: **MAC B**
- SrcMacAddr: **MAC R2p1**
- Type / Length: X
- Payload -> Data: 
	- IP src: IP A
	- IP dest: IP B
	- TTL: **62** 
		- checksum: *valor tramo3


---
# Repaso ARP

- Se usa siempre que haya una capa fisica al final del tramo
- Se lo usa a nivel corporativo para asuntos de Alta disponibilidad
	- Seguir dando servicio si se rompe uno de sus componentes
- https://www.practicalnetworking.net/series/arp/address-resolution-protocol/
	- A partir de una direccion de capa 3 conocida, quiero una de capa 2 desconocida
	- [![Pracnet.net - Address Resolution Protocol (ARP)](https://www.practicalnetworking.net/wp-content/uploads/2017/01/traditional-arp-process.gif)](https://www.practicalnetworking.net/wp-content/uploads/2017/01/traditional-arp-process.gif)
- Timing
	- ARP tambien es un mecanismo para saber si un host esta vivo o no
	- *Dest host unreachable* de ping es un paquete ARP
		- Si el host esta vivo pero filtrado por firewall da *timeout*
	- Cambios de mac address manteniendo IP es un problema porque un router podri mandar tramas a un mac addres que no existe mas (ARP timeout es muy largo
- Proxy ARP
	- Proxy es un intermediaro que hace de cliente y de servidor
	- Responde el ARP REQ
	- Se usabs para equipos que no soportaban configurar mascara, entonces los ARP REQ no le podian llegar
- Proxy ARP + NAT 
	-  [![proxy-arp-nat](https://www.practicalnetworking.net/wp-content/uploads/2017/01/proxy-arp-nat.gif)](https://www.practicalnetworking.net/wp-content/uploads/2017/01/proxy-arp-nat.gif)
- Muchos equipos tienen deshabilitado actualizar la table cache de Gratuitous ARP porque es una amenaza si alguien manda un paquete de GARP diciendo que un equipo de afuera es la default gateway (y manda todo el trafico a traves de ella)

# ICMP

## Ping
- Mediante ICMP Echo Request
- hay dos instancias de ping posibles, porque el echo request tiene identifiers distintos en cada solicitud