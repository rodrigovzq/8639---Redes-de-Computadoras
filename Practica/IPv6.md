- Surge por el agotamiento de ipv4
- segun cuan temprano hayas llegado, e asignaban mas cantidad
	- en africa hay un pais que tiene 256 sola ip
- NAPT es para parchear esto sin recurrir a ipv6
	- No es tan transparente
- BGP: protocolo de ruteo de internet
- QoS es un motivador para pasar a ipv6
	- es mas natural
- Temas de seguridad tambien son los motivantes
	- authentication header-> asegura la integridad mediante una firma
	- ESP: encapsulated security payload-> privacidad, cifra el datagrama
		- ipsec integrado
- Stateless configuration
- Paqeutes IP eficientes y extensibles
	- no hay fragmentacion en los routers
	- alineados a 64 bits
	- header de longitud fija -> facilita procesamiento
	- payload 65535
![[Pasted image 20230608180424.png]]

- Hop limit = TTL
- HDRLen desaparece
- ID FLAGS y FO desaparecen
- CHECKSUM desaparece
- OPTIONS desaparece
- traffic class: dice el tipo de prioridad
- respecto a ipv4
	- el payload se cuadruplico y el header solo se duplica
- Los header solo se examinan en destino
- no existe mas la direccion boradcast

## Fragmentacion

- Path MTU discovery
	- proceso iterativo para ver cual es el camino mas chico
	1. Se asume que el MTU del camino es el MTU del emisor local
	2. ICMPv6 si falla va a devolver *Packet too big* con la informacion del MTU del camino
	3. El proceso se repite hasta que el MTU es lo suficientemente bajo para no rebotar por Packet too big