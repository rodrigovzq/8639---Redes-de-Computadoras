## IPv4 VSLM

### IP
1. Direccionamiento
2. Ruteo
3. Fragmentacion

- Se tiene una *ruta directa* por interfaz (no siempre se cuenta la de loopback)
	- siempre tiene loopback en routers: se configura y tiene mascara de 32bit.
	- no siempre en pc
		- windows server -> Si
		- windows desktop -> No
- La ruta default `0.0.0.0`es la que matchea cuando queres salir de red (ruta indirecta)
- Router: todo dispositivo que tiene 2 o mas interfaces fisicas activas.
- HostAddr AND NetMask = NetAddr

### Plan de direccionamiento

- hosts = $2 ^{32-n}$ con n es la mascara
- se cuentan los hosts y se usa un n inmediatamente superior al que la cuenta dio
- netBlock -> direccion de base + /n 
	- direccionBase = direccionBase AND mascara(/n)
- Se ordenan por mascara de manera creciente, es decir, por tamaño decreciente
- BcastAddr = NetAddr OR not(NetMask)
- **Practica de plan de direccionamiento**

# Servicio de Transporte

Ciertas aplicaciones Client/Server conocidas como WKS tienen un **port number reservado** (<1024) que usa el **server** y los **client** usan **ephemeral ports numbers** (>=1024)

## UDP
![[Pasted image 20230417182812.png]]


- Es simple
- No es orientado a la conexion
	- Cuando el estado del mensaje depende de la interaccion pasada, hablamos de una comunicacion orientada a la conexion (logica, no fisica).
	- En ambos casos se usa `PORTs`
- Muy util, DNS trabaja sobre UDP
- Parametros
	- Source IP
	- Source PORT
	- Protocol: TCP o UDP
	- Destination IP
	- Destination PORT
- Overhead minimo -> eficiente
	- relacionado al uso de informacion en el encabezado
- Overload minimo
	- Debido al control de mensaje
- Muy rapido
- Control de flujo -> no tiene
	- Evitar que un emisor haga *desbordar* al receptor
	- Regular el flujo a medida que el receptor procesa
- Control de congestion
	- Evitar que se desborden las colas de los intermediarios
- Se usa para *ping-pong* de rapidos mensajes
- Se puede tener confiabilidad de integridad en UDP pero depende del aplicativo, no del proctolo
- Cuantos datos puede transportar un datagrama UDP
	- Limitada por IP
	- Campo lenght permite un tamaño **maximo de 64KB**

![[Pasted image 20230417174015.png]]
- Se puede configurar servicios a puertos distintos pero es **Security by Obscurity**

# TCP


![[Pasted image 20230417185409.png]]

# Adaptacion dinamica

Tiempos de retransmision RTO ajustables automaticamente

Ventanas desalizantes de tamaño variable
- control de flujo - advertised window
	- ventana de transmisor
- Control de congestion - congestion window
	- es la calculada y es del receptro

Throughput = W / RTT
Ventana/rountrip time
RTT
- Calidad de enlaces, cercania y tipo de medio (cable o satelital)
- Tiempos de propagacion
## ARQ Sliding Window
![[Pasted image 20230508173859.png]]

# Algoritmos de control de congestion

## TAHOE
- Slow Start
- Congestion avoidance
- Fast retransmit

### Slow Start 
A cada RTT, la cantidad de ACKs se duplica, RTT por lo cual la cwnd Cwnd=2(MSS) aumenta exponencialmente

![[Pasted image 20230508175830.png]]
- Al inicio de la conexión TCP, el Transmisor Tx calcula la cwnd = 1 MSS. 
- Cada vez que recibe un ACK aumenta la cwnd=cwnd+1 MSS
- Por cada RTT duplico la ventana...
- ![[Pasted image 20230508180210.png]]
- MSS = 8K , RTT = 10ms
	- 64mssx8k/10ms en bytes = 50MBps -> 410Mbps
- Cuando empieza a haber descartes masivos, ahi es el maximo
- Cuando el Transmisor Tx detecta una perdida de segmento TCP, asume que se debió a congestion severa, y reduce drásticamente la cwnd = 1 MSS, por lo cual reinicia el proceso de Slow Start.
- El Tx setea la variable ssthresh (slow start threshold) a la mitad del valor que tenia la cwnd cuando se detecto la perdida del segmento TCP.
- Cuando la cwnd >= ssthresh, el Tx pasara a “congestion avoidance” cada vez que recibe un ACK aumenta la cwnd = cwnd + 1/cwnd -> crecimiento lineal
- ![[Pasted image 20230508180649.png]]
- ![[Pasted image 20230508180837.png]]
- Ahora cada RTT se incrementa en una unidad MSS

> Como saber si la perdida de trama es por congestion o no? Para eso es el Fast Retransmit


Si la perdida de un segmento se debe a errores (ej: por ruido impulsivo),no por congestion, seguramente varios segmentos posteriores al descartado/perdido logran llegar al Rx (perdida menor al 1%) el cual comienza a enviar ACKs indicando en todos los ACKs el mismo AN (se dice que son ACKs duplicados)

**Solución**: Control de Errores con Fast Retransmit Cuando el Transmisor Tx recibe mas de 3 ACKs duplicados, asume que el segmento indicado en el AN fue descartado/perdido y retransmite los segmentos a partir del AN, sin esperar que se venza el RTO.

![[Pasted image 20230508181302.png]]
![[Pasted image 20230508181355.png]]

El receptor se guarda en memoria el ultimo segmento
- **Si recibo ACK repetidos, es que se perdio un segmento.**
	- Por ruido impulsivo
	- Congestion leve
- En cuanto veo ACK repetiros 3 veces, retransmito el segmento sin esperar a que expire el RTO.
- Esto tiene que ver con CONTROL DE ERRORES

### Fast Recovery
![[Pasted image 20230508181651.png]]

- sstrsh = cwnd/2
- cwnd = sstrsh
- Esto es control de errores tambien

Resumen
**ARQ Sliding Window**
- Slow Start
- Congestion Avoidance
- *Fast Retransmit*
- *Fast Recovery*