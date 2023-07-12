# Preguntas de UDP, TCP

## Aplicaciones distribuidas

- ¿Que entiende por IPC?
> Es un modelo de interaccion. El cliente pide y el servidor provee

- ¿En que consiste el modelo cliente&servidor utilizado por la mayoria de las aplicciones distribuidas?
	- P2P
	- Publisher-subscriber
		- Broker de valores
		- 

- ¿Que otros modelos o arquitecturas de aplicaciones distribuids conoce?

- ¿Para que se usan los "logical port numbers" de la capa de transporte?
	- Son los numeros que se usan para identificar aplicaciones, no son los procesid

- ¿Cuales son los 5 parametros que se usan para multiplexar y demultiplexar los flujos de sesiones protocolares de capa de transporte?
	- Protocolo
	- IP de A
	- Port de A
	- IP de B
	- Port de B

- ¿A que se denomina "end-point"?
	- Es el punto fisico al que se conecta para intercambio de informacion
	- un socket es un conjunto de endpoints

- ¿Que entiende por WKS? ¿Cual es la diferencia entre el termino WKS y "reserved port"?
	- Well Known Service
	- Es el servicio (como HTTP, puerto 80) que tienen puertos reservados por convencion

- ¿A que se denomina un "ephemeral port number"?
	- Los que usa el cliente que son > 1024

- ¿Cuales son los WKS mas conocidos y usados? ¿Sobre qué protocolo de transporte trabajan? ¿Que "reserved port" uilizan?
	- tablita de ppt

- ¿Qué comando se puede usar para ver la tabla de procesos udp/tcp en una plataforma de Windows? ¿Y en el caso de una plataforma linux?
	- Windows `netstat -n`
	- 



## UDP

- ¿Qué tipo de servicio de transporte ofrece UDP?
> Tipo no orientado a la conexion, no garantiza la entrega confiable de los datos ni el control de flujo ya que no establece conexion previa a enviar los datos

- ¿Qué ventajas ofrece el transporte UDP frente a TCP?
> Es mas rapido
> Menor sobrecarga: porque no tiene que hacer seguimiento de los paquetes ni establecer conexiones

- ¿Qué funcionalidades no son soportadas por UDP? (en comparación con TCP)
> Control de flujo
> Control de congestion
> Confiabilidad e integridad

- ¿Cuál es el nombre de las PDUs UDP?
> Datagrama

- Dado que el datagrama UDP está encapsulado en un datagrama IP, ¿cuál puede ser su tamaño máximo?
> Segun el maximo numero admitido en el campo length: 64KB

- En el caso de que IP necesite fragmentarse, ¿en qué fragmento se transmitirá el encabezado UDP?
> En el primero

- ¿Cuáles son los campos más relevantes del encabezado UDP?

> Source Port
> Destination Port
> Lenght
> Checksum
> ![[Pasted image 20230417182908.png]]
> 

- ¿Cuáles son los WKSs UDP más populares? ¿Qué números de port tienen reservados?
> DNS (53)
> DHCP (67 server, 68 cliente)
> SNMP (161, 162)
> NTP (123)
> RTP usa UDP pero no usa port reservados

![[Pasted image 20230417174036.png]]




## TCP

### FUNCTIONS, HEADER, SEGMENTATION

- ¿Conoce las funciones de TCP y puede explicar el proceso de comunicación?
> TCP es un protocolo de transporte  extremo a extremo que se utiliza para proporcionar una conexión confiable, orientada a la conexión y bidireccional entre dos dispositivos en una red. TCP garantiza que los datos se entreguen en orden y sin errores, y que cada paquete de datos se confirme su recepción.
> TCP es un pipestream, flujo de bytes, no delimita mensajes como UDP.
> El proceso de comunicación utilizando TCP se puede describir en las siguientes etapas:
> 	Establecimiento de la conexión: Para iniciar una comunicación TCP, el emisor envía un paquete SYN (sincronización) al receptor, solicitando establecer una conexión. El receptor responde con un paquete SYN-ACK, indicando que está listo para establecer la conexión. Finalmente, el emisor envía un paquete ACK para confirmar la conexión.
> 	Transferencia de datos: Una vez establecida la conexión, los dispositivos pueden comenzar a transferir datos. Los datos se dividen en segmentos de tamaño fijo y se envían en paquetes individuales. Cada paquete se numerará y se confirmará su recepción
> 	Finalización de la conexión: Cuando se completa la transferencia de datos, uno de los dispositivos envía un paquete FIN para indicar que ha terminado de enviar datos. El otro dispositivo responde con un paquete ACK, confirmando que ha recibido el paquete FIN. Luego, el otro dispositivo envía un paquete FIN y el primer dispositivo responde con un paquete ACK.
> TCP también realiza varias funciones importantes durante la comunicación, incluyendo:
> 	**Segmentación** y reensamblaje de datos en paquetes individuales para su transmisión en la red.
> 	Establecimiento y finalización de conexiones entre dispositivos.
> 	Control de secuencia: garantiza el orden
> 	**ARQ Sliding Window**: es un mecanismo en realidad y es el encargado de Control de secuencia, control de error, de flujo y congestion
> 	Control de flujo para garantizar que los dispositivos no envíen más datos de lo que el receptor puede procesar.
> 	Control de congestión para evitar que se sature la red.
> 	Reordenamiento de paquetes para asegurarse de que los datos se entreguen en el orden correcto.
> 	Confirmación de recepción de paquetes para garantizar que los datos se entreguen correctamente y sin errores.
- ¿Conoce la estructura del encabezado TCP y puede explicar los campos?
![](https://www.lifewire.com/thmb/x5OJM3NzZ0ARCsU1Jtay-vt_9Gw=/750x0/filters:no_upscale():max_bytes(150000):strip_icc()/tcp-headers-f2c0881ea4c94e919794b7c0677ab90a.jpg)

> Source port
> Destination port
> Seq Number:Indica el número de secuencia del primer byte del segmento actual.
> Ack number: Indica el número de secuencia del próximo byte que espera recibir el emisor.
> Longitud de cabecera: Es el tamaño de la cabecera del segmento, en palabras de 32 bits. Se utiliza para identificar el comienzo de los datos de usuario.
> Bandera de control: Las banderas de control son usadas para controlar la comunicación entre los dispositivos. Las banderas de control más importantes son las siguientes:
> 	 `URG` (Urgente): Indica que el segmento contiene datos urgentes que requieren una atención inmediata.
> 	 `ACK` (Acknowledgment): Indica que el segmento contiene un acuse de recibo válido.
> 	 `PSH` (Push): Indica que el receptor debe entregar los datos a la capa de aplicación de destino sin esperar a que se completen los demás datos del paquete.
> 	 `RST` (Reset): Se utiliza para reiniciar una conexión TCP de forma inmediata.
> 	 `SYN` (Synchronize): Se utiliza para iniciar una conexión TCP.
> 	 `FIN `(Finalize): Se utiliza para finalizar una conexión TCP.
>  Window size: advertised windows por el receptor
>  Checksum
>  Urgent Pointer
> 	 Dice en que posicion del payload empiezan los datos urgentes. Normalmente estan al final
> 	 Esto es porque TCP permite datos no secuenciados
> 	 
- ¿Cómo se llama la PDU TCP? ¿Por qué?
> **Segmento**. Porque es una porcion de un flujo de datos.

- ¿En qué capa se encapsulan los segmentos TCP?
> en IP se encapsulan. Capa 3

- Si el segmento es más grande que la MTU de la red y debe fragmentarse, ¿en qué fragmento de ip se transmitirá el encabezado tcp?
> En el primero

- ¿Qué significa MSS? ¿En que momento se establece el MSS?
> Maximum Segment Size: teoricamente es 64KB de maximo
> En el momento de establecimiento de la conexion (en el SYN)


### FULL DUPLEX

- ¿Está claro el concepto de full-duplex? (2 flujos, cada entidad tcp tiene un Tx y un Rx)
> el concepto de full-duplex se refiere a la capacidad de una conexión de red para transmitir datos en ambas direcciones al mismo tiempo. En una conexión full-duplex, cada entidad TCP (por ejemplo, un dispositivo de red) tiene dos flujos de datos separados, uno para la transmisión (Tx) y otro para la recepción (Rx), lo que significa que puede enviar y recibir datos simultáneamente.



- ¿Qué campos del encabezado corresponden al flujo de origen a destino (enviado por el Tx)?
> El se secuence number

- ¿Qué otros campos corresponden al flujo destino a origen (enviado por el Rx)?
> Lo que hay disponible del buffer luego de haber recibido un mensaje, es el dato que va en la ventana. Eso actua de control de flujo.
> Hay extrangulamiento cuando se envia un Window size = 0, el host que envia eso es el agotado


### CONNECTION ORIENTED

- ¿Sabes cómo es el proceso de conexión y desconexión?
> 3 way handshake
> 	SYN
> 	SYN-ACK
> 	ACK
> 	![[Pasted image 20230417183952.png]]
> 	ACK: es el numeero del proximo SEQN que espero. Es decir que recibi SEQN-1

- ¿Por qué TCP es un protocolo orientado a la conexión?
> Porque para saber que hacer con un mensaje, se evaluan condiciones pasadas por lo que se necesita una conexion.

- ¿Cuáles son los estados en los que puede estar la máquina de estados o máquina de protocolo TCP?
	- Closed, listen y established.
	- Los demas son temporarios
> ![[Pasted image 20230417185152.png]]


- ¿En qué estado debe estar la entidad TCP para intercambiar datos en dúplex completo?
	- Ambos en **ESTABLISHED**
	- Porque en el resto de los no temporarios hay intercambio en un solo sentido (half duplex)

- ¿Cuántos segmentos se necesitan para establecer una conexión tcp?
> 3, en el segundo se intercambian a la vez en ambos flujos

- ¿Qué flags de control se utilizan?
> el ACK y el SYN

- ¿Qué parámetros iniciales se configuran durante el establecimiento de la conexión?
	- inital seq number

- ¿Cuántos segmentos se necesitan para cerrar una conexión tcp?
> Normalmente se intercambian 4
> ![[Pasted image 20230417185317.png]]

- ¿Qué flags de control se utilizan?
	- ACK y FIN



### INTEGRITY CHECK 

- ¿Qué le puede pasar a un segmento tcp enviado por la red ip?
	- Se puede perder y no me llega, corromper y el checksum da mal
	

- ¿Para qué se utiliza el checksum? ¿En qué casos es útil?
	- Para veriricfar la integridad del segmento
	- - el checksum sirve para saber si el segmento fue alterado en el camino
		- solo **alterados** detecta



### SEQUENCE CONTROL

- ¿Cuál es el campo del encabezado tcp que se usa para secuenciar los datos recibidos en el rx?
	- SEQ Numnber
	- Los mensajes no estan numerados en forma secuencial contigua sino que SN= SN-1 + DataLength
	- Resuelve el duplicado porque lo descarta

- ¿Qué indica el SN, el número de secuencia del segmento o el número de secuencia del primer octeto contenido en el segmento?
	- El numero de secuencia del primer octeto



### ARQ Y CONTROL DE ERRORES
Automatic Repeat on Query

- ¿Cómo se hace el control de errores?
	- ![[Pasted image 20230424175323.png]]
	- Gracias al 3Whandshake pueden calcular el RTT inicial
	- Cada segmento enviado tiene un SN y transporta DL bytes
	- Se transmiten los datos, se secuencian, si despues de RTO no llega nada, retransmito
	- 


- ¿Qué significa AN? ¿Qué indica AN?
	- Al recibir sin errores los DL con SN=X, el receptor confirma los datos recibidos indicando el *proximo numero de secuencia que espera al recibir* contestando con un AN=X+DL

- ¿Cuáles son los parámetros ARQ que son variables y se adaptan dinámicamente?



- ¿Qué es el RTO?
	- ![[Pasted image 20230424181854.png]]
	- Es el tiempo en el cual se espera a recibir la confirmacion, pasado este tiempo se retransmite la secuencia

- ¿En base a qué se ajusta dinámicamente el RTO?
	- Advertised Window: Datos que puedo transmitir a partir del proximo SN que el receptor me dice que esta esperando recibir
	- Congestion Window: Si la AW es mayor es este valor, se envian CW datos para no congestionar

- ¿Qué pasaría si el RTO fuera mucho más alto que el RTT?
	- Se usaria muy poco el canal de comunicacion

- ¿Qué pasaría si el RTO fuera igual o menor que el RTT?
	- Se retransmitira innecesariamente, porque reaccionas antes de que te llegue el ACK

- ¿Entiende el significado del algoritmo con el que el Tx calcula el RTO en base al RTT medido?
	- ecuaciones que se ejecutan por software para calcular las ventanas



### ARQ Sliding Window

- ¿Podría explicar el principio de la gestión de ventanas TCP?
	- Es por una cuestion de rendimiento en el uso del canal
	- Puede ser igual o menor al advertised
	- Si es igual, es que es el receptor y aesto se lo llama control de flujo
	- Permite aprovechar todo el ancho de banda sin haber recibido confirmacion (datos que puedo recibir sin confirmacion = tamaño de ventana)



- ¿Qué significa el tamaño de la ventana?
	- Es la cantidad de bytes que puedo trasnmitir a partir de un numero de secuencia

- Si el Tx recibe un segmento con AN=1000 y W=10000, ¿cuáles son los números SN que podrá transmitir sin esperar nueva confirmación y ventana?
	- 1000 a 10000-1000-1
	- De AN hasta AN+W-1

- ¿Cómo puede calcular el throughput máximo en función del tamaño de la ventana y el RTT?
	- T=W/RTT

- ¿Cuántos bits tiene la ventana? ¿Cuál es el tamaño máximo de una ventana?
	- 16 bits
	- El campo window lo completa el receptor y el transmisor la usa

- Con un W de 16 bits (W<64kiB) y un RTT de 64ms, ¿cuál es el throughput máximo que se puede lograr?

- ¿Qué limitación impone una ventana de 16 bits? ¿Es posible utilizar ventanas más grandes? ¿Cuántos bits?



- ¿Está familiarizado con el producto Bandwidth Delay y puede explicar su importancia para el control de sobrecarga mediante el control de ventana?

- ¿Qué se entiende por producto de retardo de ancho de banda (CBD)?

- ¿Qué pasa si la W es más baja que la CBD?

- ¿Qué son las LFT de Long Fat Networks?

- ¿Cuál es el problema con los LFT?

- ¿Cómo resolver el problema de LFT con TCP?



### CONTROL DE FLUJO

- ¿Conoce los métodos para el control de sobrecarga de TCP? ¿Control de flujo? ¿Control de congestión?
	- ARQ Sliding Windows. CF cuando la limitacion es la cola del otro extremo. CC es cuando la lmitacion es el medio de la red

- ¿Qué cola evita sobrecargar el mecanismo de control de flujo?
	- El buffer del receptro

- Se dice que el control de flujo es explícito. ¿Por qué?
	- Porque el receptor le indica la cantidad de bytesdisponibles para recepcion.
	- Advertised windows. 
	- Se lo dice en el ACK

- ¿Cuál es la Advertized Window? ¿Qué representa la awnd del búfer de recepción?
	- ACL AN = X + W
	- Es la capacidad disponible en el buffer de recepcion

- ¿Qué sucede cuando awnd=0?
	- El buffer de Rx esta lleno y el transmisor no puede seguir transmitiendo



### CONGESTION CONTROL

- ¿Cuáles son las colas que se evitan sobrecargar con el mecanismo de control de congestión?
	- Las de los routers o switches (capa 2)
	- conjestion suave: alarga cola sin sobrepasarse
	- Conjestion severa: alarga la cola con sobrepase
	- Se detecta la perdida de segmentos y asumimos congestion -> bajar el tamaño de la ventana

- ¿Qué es la Congestion Window?
	- Es la ventana que calcula el transmisor en funcion de lo que interpreta que ocurre en la red
	- 



- ¿Podría explicar la determinación de la cwnd con Slow Start y Congestion Avoidance según Van Jacobson?
	- SS empieza cwnd exponencial hasta perder segmentos
	- CA crece linealmente hasta crecer
	- FA

- ¿Por qué la conexión tcp comienza con cwnd=1MSS?
	- tiene que empezar al minimo para detectar la capacidad maxima del path entre los hosts

- ¿Cómo crece la cwnd en la fase de Slow Start?
	- Exponencialmente

- ¿Cómo crece la cwnd en la fase de Congestion Avoidance?
	- Linealmente

- ¿Bajo qué condición el algoritmo de incremento de cwnd cambia de crecimiento exponencial a crecimiento lineal?
	- Cuando alcanza el ssthrs

- ¿Qué hace el Tx con el cwnd y el ssthreshold cuando detecta una pérdida de segmento debido a RTO?
	- Hay congestion severa
	- Retransmite 
	- cwnd = 1MSS
	- sshrtesh a la mitad de la que estaba



- ¿Conoce los métodos de FAST Retransmit y FAST Recovery y puede explicarlos?
	- Si se repiten los ACK 3 veces, se retransmite antes del RTO
	- FReco baja la cwnd a sshthres en vez de 

- ¿Cómo funciona el Tx para retransmitir más rápido un segmento perdido usando ANs?
	- Retransmite a partir del ACK repetido

- ¿Qué hace el Tx con cwnd y ssthreshold cuando detecta una pérdida de segmento debido a 3DupAck?
	- sshtrhesl lo baja a la mitad del cwnd que tenia
	- cwnd = ssthresghold

- ¿Por qué el Tx cuando detecta 3DupAck reduce cwnd=ssthres en lugar de reducirlo a cwnd=1MSS?
	- Porque la congestion es leve o porque se perdio el segmento no necesariamente por congestion