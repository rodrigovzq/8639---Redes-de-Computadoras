# Ethernet LAN Switching
1. Indique Verdadero o Falso. Justifique cada una de sus respuestas falsas.
Sean dos hosts H1 y H2 conectados a una red LAN Ethernet/IEEE 802.3. En un momento dado, H1 envía una trama con el MAC address destino de H2, la trama ocupa el canal sin generar colisiones en la red, pero al ser interpretada por H2 da un error de CRC. Esto significa:
* **V**-que H2 descartará la trama por no ser válida para enviar a las capas superiores.
	* Ethernet 802,3 descarta la trama
* **F**- que H2 generó una colisión.
	* CRC es que la trama fue corrupta en datos. si hay colision no recibis nada
* **F**-que H2 pedirá a H1 un reenvío de la trama fallada.
	* Ethernet no solicita reenvio porque no tiene mecanismo de control de flujo ni correccion de errores como TCP
* **V**- que hubo un error de al menos 1 (uno) bit en la interpretación de la trama por H2.
	* El checksum es el CRC y hace una suma xor de los datos de la trama para calcular el CRC
* **F**- que H2 pedirá por medio de un broadcast MAC el reenvío de la trama ya que no pudo leer el address MAC origen de la misma.
	* Ethernet no tiene control de flujo
* **F**. que H1 duplicará su tiempo de espera de intento de retransmisión de 51,2 us.
	* esto es cuando hay colision, no CRC
* **F**. que sólo las capas superiores de protocolo negociarán una retransmisión ya que, visto desde la capa MAC de H1, la transmisión de la trama fue exitosa.
	* no hay retransmision**


2. Indicar cuáles de las siguientes afirmaciones son ciertas con un check **X** cut-through y fragment-free son dos tecnologías que
- **Aumentan el throughput de paquetes** 
	- Aceleran el reenvio de paquetes
- **Reducen la latencia**
	- No esperan a que se complete la recepcion
- Minimizan las colisiones
	- al contrario
- **Adaptan velocidades**
	- son tecnicas de switcheo como S&F asi que si. Cut Through envia a la velocidad de la interfaz de entrada.


3. Indique Verdadero o Falso. Justifique cada una de sus respuestas.
- **V** . un switch que soporta VLANs puede ser unmanaged
	- los unmanaged no tienen concepto de VLAN pero aun asi puede ser parte de una VLAN configurada en otro lado
- **F** Ethernet con CSMA/CD puede utilizarse para comunicar aplicaciones de tiempo real críticas (tiempo acotado garantizado)
	- Porque el mecanismo de deteccion de colsiones no puede garantizar tiempos de entrega acotados
- **F** La BPDU se encapsula sobre IP
	- va directo sobre trama Ethernet
	- IP se encapsula en Ethernet y no al revés 
- 2 BPDUs provenientes de un mismo switch recibidas por distintos puer- tos pueden empatar y entonces el switch receptor eligirá una vencedora al azar.
	- el receptor compara los ID de bridge y root path cost, el mas bajo sera  la seleccionada
- El árbol generado por el Spanning Tree Protocol depende del orden en que se hayan encendidos los equipos y de cuando se hayan conectado los uplinks entre switches
	- **Falso** el algoritmo tiene en cuenta la topologia fisica, la prioridad de los swithces

4. Dados los siguientes 2 switches cuál elegiría adquirir en base a un criterio que considere características técnicas (es decir: no considere marcas, soporte post-venta, arreglos comerciales corporativos)
![[Pasted image 20230517193948.png]]
> Si el trafico es de alto volumen y pocos terminales conectados, mas velocidad de backplane, si es de menor volumen elegiria el 2 que tiene mayor velocidad de forwarding

5. (STP) Un usuario de la red nos hace notar que cada vez que conecta su notebook a la boca de red de la LAN, éste no puede cursar tráfico durante un breve plazo de tiempo. ¿Cuál sería una posible explicación? ¿Cómo se podría calcular dicho tiempo?

> Es por el tiempo que se recalcula el STP para considerar el nuevo host en la red antes de darle IP.

6. (STP) ¿Cuál es el riesgo de no activar STP en las bocas de red de los usuarios? ¿Cuál es el riesgo de activarlo?
> El riesgo de no activarlo es que podrian aparecer bucles si se conectaran varios enlaces entre switches y el riesgo de activarlo es causar una interrupcion temporal en la red para recalcular el STP cuando se conecta un host nuevo y asi se podrian causar perdida de paquetes


7. Cuáles son las funcionalidades propias del repeater, del switching/bridging y del routing? Arme una tabla comparativa.

**HUB**
- S&F: No
- Adapta velocidades: No
- Filtrado: No
- No Match: No
- Separa dominios de colision: No
- Separa dominios de bcast: No
- Loops: No

**Switch**
- S&F: Si
- Adapta velocidades: Si
- Filtrado: via MAC
- No match: Flooding (envia paquete a traves de todas las interfaces)
- Separa dominios de colision: Si
- Separa dominios de bcast: No
- Loops: No

**Router**
- S&F: Si
- Adapta velocidades: Si
- Filtrado: via IP
- No match: Droping (baja la velocidad cuando hay congestion)
- Separa dominios de colision: Si
- Separa dominios de bcast: Si
- Loops: Si

8. ¿Cómo se resuelve el forwarding si los ports de entrada y salida de tramas Ethernet tienen distintas velocidades? 
> Se resuelve mediante el mecanismo de buffering. El switch almacena temporalmente la trama recibida y la envia a la velocidad establecida por el puerto de salida. De esta manera no se pierden paquete pero afecta al rendimiento del switch ya que aumenta la latencia y puede generar congestion en la red


9. ¿Por qué es necesario “abrir los loops” en topologías malladas cuando se hace bridging/switching? ¿Qué protocolo se utiliza?
> Para que las tramas no se forwardeen de manera ciclicla y para evitar el *broadcast storm* (paquetes broadcast circulando en loops), utilizaria el  STP para calcular caminos de menos costo y abrir los loops de manera logica

10. En el caso de segmentar tráfico en VLANs, ¿cómo se hace para hacer el forwarding entre hosts de distintas VLANs? ¿Se puede hacer esto en el mismo Switch?
> Para hacer forwarding entre hosts de distintas VLANs se necesita un dspositivo de capa 3 como un router. Si estan en el mismo swtich, se puede hacer que este actue como router, esto se llama enrutamiento inter-VLAN pero como un switch no es capa 3, va a tener menor rendimiento y no todas las caracteristicas de un router


# IP/ICMP/ARP


1. Describa co ́mo funciona el utilitario PING. ¿Cómo es que puede haber dos instancias del programa PING en una misma PC apuntando a una misma IP destino y los programas no confunden las respuestas entre sí?
> El comando ping se utiliza para verificar conectividad de un host hacia otra utilizando paquetes de solicitud ICMP
> 	H1 ejecuta comando ping y crea un paquete ICMP de solicitud (ICMP Echo Request) y lo envia al despito IP de H2
> 	H2 recibe y genera un paquete de respuesta (ICMP Echo Reply)
> 	La respuesta se envia con IP destino al origen del REQ
> 	H1 muestra informacion de tiempo de ida y vuelta RTT, perdida de paquetes, etc
> El poder tener dos instancias de ping que no se confundan es porque cada instancia de ping genera un PID unico en el sistema, esto permite que las respuestas se asignen de manera correcta a cada instancia

2. Describa cómo podría determinar el MTU del camino (path MTU) atrave- sado entre dos IPs utilizando el programa PING.
> Se podria hacer ejecutando en serie comandos ping con tamaño de datos creciente y el MTU se puede ver cuando en las respuestas se recibe "Paquete demasiado grande" de ICMP y en este se ajusta el tamaño del paquete al valor del MTU.

3. Desarrollar: ARP es un protocolo general y no exclusivo de IP.
> ARP (Adrress Resolution Protocol) es un protocoo de resolucion de direcciones utilizado en redes LAN para asociar direcciones fisicas (MAC) con direcciones logicas (IP). Aunque ARP se utiliza normalmente en redes que implementan IP, no esta limitado a IP ya que trabaja a nivel de enlace de datos del modelo OSI (capa 2)

4. Enumere los campos del datagrama IP que pueden ser modificados en el tránsito por un router.
> TTL
> Flags
> 	Fragmentation: DF, Frag ID
> Fragment offset
> Checksum

5. ¿En qué casos un mensaje ICMP puede generar otro mensaje ICMP?
> Un Echo REQ genera un REPLY
> cuando un dispositivo manda ECHO REQ y se genera Destination unreachable

6. ¿Qué diferencia hay entre hacer Subnetting de Máscara Fija y VLSM? ¿Cuál de ellas soporta el ruteo Classful?
> Se usa FLSM cuando se agrupa hosts en grupos que tengan la misma cantidad de hosts, es decir, se tiene una unica mascara para todos y VLSM (solo soportado en Classless) cuando se necesite agrupar con una cantidad diferente de hosts entre grupos.
> FLSM es direccionamiento y VLSM es ruteo

7. ¿Para qué sirve y en qué consiste la “agregación de rutas”? Dé un ejemplo.
> Route summarization es una tecnica que se utiliza para reducir la tabla de ruteo y la complejidad de la misma, consiste en reducir el numero de la mascara  y conservar el next hop, de esta manera agrupando a varias redes en una sola entrada de la tabla de ruteo
> Ejemplo:
> las subredes 192.168.1.0/24, 192.168.2.0/24 y 192.168.3.0/24 en la sucursal A, en lugar de anunciar estas tres subredes por separado, puedes resumirlas en una sola ruta de 192.168.0.0/16.

8. Describa el proceso de ruteo CIDR.Indique cómo prioriza las rutas en función de la máscara y de la métrica.
- Recibe el datagrama y lee su DestAddr
- Si la DA es la de alguna interfase local, entrega el datagrama a la capa superior indicada en **Protocol**
- Si no, recorre la talba de ruteo en orden decreciente (de mas especifica a menos) de RouteMask buscando matchear una ruta
	- DestAddr AND RouteMask == RouteDestination
- cuando la DestAddr matchea, reenvia el datagrama por esa ruta
- Si no matchea con ninguna, descarta el datagrama o se manda por default gateway si tuviera.
- Si matchea mas de una ruta, usa la de mayor mascara (la mas especifica)


9. ¿En qué consiste el Proxy ARP? Dé un ejemplo de utilizacio ́n.
> se da cuando el ARP  REQ es repondido por otro host (no el que posee la IP destino en el REQ). Se usaba cuando un host no soportaban configuracion de mascara entonces no le podian llegar los ARP REQ

10. ¿Qué campos del header IP se pueden utilizar para hacer Policy Based Rou- ting ?
* Source y destination address
* Protocol: se puede usar para aplicar politicas basadas en el servicio requerido

11. ¿Qué hace un Router si para un determinado datagrama IP se decrementa su TTL y este llega a 0? ¿Qué mensaje ICMP envía y a quién?
> se envia el mensaje ICMP de error *Time Exceeded* code 0: TTL expired in transit


# UDP / TCP

1. Responder verdadero o falso, justificar las falsas
a. El primer datagrama de una conexión TCP setea el bit SYN y el ACK
para iniciar la conexión.
	**Falso**
	El primer SEGMENTO que se envia tiene las variables SYN y el MSS (Maximun segment size), no se setea el ACK sino que este se envia en la respuesta y en esa respuesta se envia X+1 siendo X lo que se envio en SYN
b. La PDU de TCP es denominada fragmento
	**Falso**
	Se denomina SEGMENTO
c. UDP siempre implementa un mecanismo de verificación de errores del
header IP
	**Falso**
	UDP es un mecanismo de transporte sin conexion ni es confiable, los mecanismos de veririficacion de errores deben correr en el aplicativo que este en capas superiores. El mecanismo de checksum puede servir para verificar errores en la integridad de los datospero es opcional y no es del header IP
d . El tamaño de un segmento TCP es fijado por la aplicación que lo genera
	**Falso**
	el tamaño maximo de un segmento TCP esta determinado por el payload de un datagrama IP, va a depender del mtu de la red
e. En Congestion Advoidance el crecimiento de la ventana es 1/cwnd MSS
por cada ACK recibido
	**Verdadero**
	Congestion Avoidance comienza cuando
	`cwnd >= ssthrsh`
	Por cada *ACK* correcto:
	`cwnd <- cwnd + 1/cwnd`
	*Crecimiento Lineal* de cwnd
	cada RTT: `cwnd <- cwnd + 1`
f . La duración del valor de “time out” del temporizador de retransmi-
sión de TCP depende del RTT de los segmentos (sin retransmisiones)
previamente transmitidos.
	**Verdadero**
	En el caso de perdida de segmento, despues de un tiempo RTO el transmisor retransmite a partir del ultimo AN indicado por el receptor.
	El RTO es dinamico y estimado en base al RTT
	$R_{(n)}= \alpha R_{(n-1)} + (1-\alpha) RTT$
	$RTO=R.\beta$
	$\alpha$ es un smoothing factor entre 0 y 1, tipicamente 0.5
	$\beta$ es un factor de varianza del delay mayor a 1, tipicamente 2
	tipicamente seria $RTO= R_{(n-1)} +  RTT$
	
g. El cliente de una aplicación TCP utiliza ports menores a 1024 denomi-
nados well known ports
	**Falso**
	El cliente usa puertos mayores a 1024 , el servidor usa los menores y se llaman *reserved ports* o *well known services*
h. Si un segmento TCP llega con error a su destino, es simplemente des-
cartado.
	**Falso**
	No solamente se descarta sino que se envia un ACK con los valores de numero de secuencia previos a la recepcion del segmento con error, en definitiva enviando un pedido de retransmision.
	
i. El checksum de UDP es opcional y se indica con un valor de checksum
igual a 0
	**Verdadero**
j. El pseudo header de UDP utilizado para calcular el checksum incluye
los primeros 64 bytes de datos
	**Falso**
	Se incluyen todos los datos en el pseudoheader
k. El cliente de una aplicación UDP utiliza ports mayores a 1024 denomi-
nados well known ports
	**Falso**
	Es cierto que los clientes usan los puertos mayores a 1024 pero se llaman *ephemeral ports*
l. Si un datagrama UDP llega con error a su destino, este ´ultimo solicita
un pedido de retransmisión.
	**Verdadero**
	Se reenvia el ACK con el numero de SYN que se recibio correctamente y el transmisor retransmite desde alli, efectivamente actuando como un pedido de retransmision
2. ¿Qué ventanas utiliza TCP? Describa su funcionalidad
	1. En ARQ Sliding window se usa
		1. advertised window: El receptor envia la W awnd indicando la cantidad de bytes que el transmisor puede enviar a partir del AN
		2. congestion window: El transmisor calcula una cwnd en funcion de una deteccion implicita del estado de congestion de la red. Cuando el Tx deteca la perdida de un segmento, asume que fue descartado por congestion severa por lo que reduce drasticamente el throughput reduciendo la cwnd. A medida que va recibiendo ACK, va aumentando la cwnd. Sliding window va tomando W=min(awnd,cwnd)
3. Explique qué es Fast Retransmit y Fast Recovey.
	1. **Fast Retransmit**: Es un mecanismo de control de congestion,Cuando el transmior recibe msa de 3 ACK duplicados, asume que el segmento indicado en el AN fue descartado o perdido (el Rx pide retransmision) y retransmite los segmentos a partir del AN que recibio duplicado, *sin esperar que se venza el RTO*. De otro modo, esperaria RTO segundos hasta tener que retransmitir
		1. Retransmision normal
		2. ![[Pasted image 20230628211954.png]]
		3. Fast Retransmit
		4. ![[Pasted image 20230628212021.png]]
	2. **Fast Recovery**: Es un mecanismo de control de congestion, cuando el transmisor hace Fast Retransmit, baja la *cwnd* al valor de *sshthersh*, osea a la mitad de la cwnd que tenia cuando recibio los ACK duplicados
4. ¿Qué funcionalidades agrega TCP respecto de UDP? ¿Cuáles serían las desventajas de TCP respecto de UDP?
	1. TCP agrega
		1. Transmision Byte Oriented Full Duplex (UDP es half)
		2. Control de secuencia
		3. ARQ Sliding window
		4. Control de errores
		5. Control de flujo explicito
		6. Control de congestion implicito
	2. Las desventajas que todas estas caracteristicas requieren mas overhead, las conexiones por TCP tienen mas latencia y son de menor rendimiento en redes de bajas prestaciones
		1. Otra desventaja es que algunas aplicaciones como el streaming requieren de retransmisiones rapidas y con UDP lo pueden controlr
5. ¿Qué mecanismo emplea TCP cuando se inicia una conexión para evitar
congestionar la red? Describalo.
	El mecanismo de Slow Start, al inicio de la conexion TCP el Tx calcula la cwnd = 1 MSS y cada vez que recibe un ACK aumenta en cwnd = cwnd + 1 MSS
6. Calcular el máximo throughput (en bits por segundo) que se podría alcan-
zar en una conexión TCP con una advertised window máxima de 8000 bytes,
y un Round Trip Time = 20 ms. Considerar que no se produce limitación por
velocidad de serialización y que en la red no se produce congestión. Explicar porque se produce esta limitación.

Throughput = W / RTT = 8000 bytes / 20 ms = 64000 bits / 20 ms= 3200 kbps