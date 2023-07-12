# 1
Respuesta correcta
La respuesta correcta es: ¿A que se denomina un "ephemeral port number"? → Un "ephemeral port number" es un port number >= 1024. En los WKS de tipo Client/Server, el proceso cliente usa un ephemeral port., ¿Que entiende por IPC? → IPC Inter Process Communication: comunicacion entre procesos aplicativos que corren en plataformas o sistemas multitasking multiusuario., ¿Cuales son los 5 parametros que se usan para multiplexar y demultiplexar los flujos de sesiones protocolares de capa de transporte? → Para el multiplexado del trafico IPC se usan: la direccion origen y destino, el protocol number, el port origen y destino.,
¿Qué comando se puede usar para ver la tabla de procesos udp/tcp en una plataforma abierta como Windows o linux? → netstat -a, ¿Que entiende por WKS? ¿Cual es la diferencia entre el termino WKS y "reserved port"? → WKS: Well Knon Service. Es un servicio o aplicacion "conocido". Ciertos (no todos) WKS de tipo Client/Server usan Reserved Port para identificar en que port escucha el server.,

¿En que consiste el modelo cliente&servidor utilizado por la mayoria de las aplicciones distribuidas? → En el modelo cliente-servidor, la interaccion entre los procesos es asimetrica: el servidor esta siempre escuchando la consulta o pedido que pueda venir de un cliente, y es el cliente el que inicia la interaccion con el servidor., ¿Para que se usan los "logical port numbers" de la capa de transporte? → Los Port Numbers se usan para multiplexar el trafico IPC. Tanto UDP como TCP usan port number para soportar esta funcionalidad., ¿A que se denomina "End-Point"? → El End Point es el par de direccion-port usado en cada End System. Todo flujo IPC queda identificado por el Protocol y los 2 End Points extremos., ¿Que otros modelos o arquitecturas de aplicaciones distribuidas conoce? → Otros modelos de aplicaciones distribuidas: Peer to Peer, Publisher-Subscriber,

¿Cuales son algunos de los WKS mas conocidos y usados? ¿Sobre qué protocolo de transporte trabajan? ¿Que "reserved port" uilizan? → DNS, UDP&TCP, 53 - HTTP, TCP, 80 - SMTP, TCP, 25 - TELNET, TCP, 23 - SSH, TCP, 22
# 2
La respuesta correcta es: ¿Cuál es el nombre de las PDUs UDP? → En UDP, al mensaje (PDU) se lo denomina "datagrama" en clara alusion a tipo de servicio de envio simple de mensajes., ¿Cuáles son los WKSs UDP más populares? ¿Qué números de port tienen reservados? → DNS 53 - SNMP 161 y 162 - RTP (no tiene reserved ports), ¿Qué tipo de servicio de transporte ofrece UDP? → El User Datagram Protocol ofrece un servicio de intercambio de mensajes de tipo "datagram", o sea envío simple de mensajes, sin verificaciones ni controles., ¿Qué funcionalidades no son soportadas por UDP? (en comparación con TCP) → UDP solo envia mensajes (datagramas) encapsulados en paquetes (datagramas) IP. UDP no da ningun tipo de acuse de recibo (Ack), ni retransmite mensajes, ni evita que las colas se desborden., En el caso de que IP necesite fragmentar, ¿en qué fragmento se transmitirá el encabezado UDP? → En caso de producirse fragmentacion IP, el header de UDP es transportado en el 1er fragmento., y no figura en los demas fragmentos.,
¿Qué ventajas ofrece el transporte UDP frente a TCP? → UDP es mas simple que TCP, por ende sobrecarga menos la red y los end systems. Es mas conveniente para aplicaciones que intercambian pocos datos y son de tipo "transactivas"., Dado que el datagrama UDP está encapsulado en un datagrama IP, ¿cuál puede ser su tamaño máximo? → El tamaño maximo de un datagrama UDP esta limitado por el tamaño máximo admitido por IP, o sea 2^16 Bytes., ¿Cuáles son los campos más relevantes del encabezado UDP? → En el header UDP se indica: Source Port, Destination Port, Length y Cheksum.
# 3
Respuesta correcta
La respuesta correcta es: ¿Cómo se llama la PDU TCP? ¿Por qué? → La PDU de TCP es llamada "segmento". Hace alusión al mecanismo/funcionalidad de segmentacion del data byte stream., Si el segmento es más grande que la MTU de la red y debe fragmentarse, ¿en qué fragmento de ip se transmitirá el encabezado tcp? → En el caso que haya que fragmentar en la capa IP, el header TCP sera transmitido (solo) en el 1er fragmento, ¿Cuales son las funciones de TCP? → Multiplexado, Full duplex Transmisión Byte Oriented , Segmentación, Control de secuencia, ARQ Sliding Window, Control de errores, Control de Flujo explícito, Control de Congestión implícito,
¿Cuales son los campos mas relevantes del encabezado TCP? → Src y Dst Port, SN, AN, SYN, ACK, FIN, W, Checksum, Options, ¿Qué significa MSS? ¿En que momento se establece el MSS? → MSS: Maximum Segment Size, es el tamaño maximo de de cada segmento. Se establece en el 3 way handshake, y se establece 1 MSS para cada flujo., ¿En qué capa se encapsulan los segmentos TCP? → El Segmento TCP es entregado a la capa IP, la cual, si hiciera falta fragmenta y encapsula en el payload del datagrama IP.
# 4
Respuesta correcta
La respuesta correcta es: ¿Cuáles son los estados en los que puede estar la máquina de estados o máquina de protocolo TCP? → Los estados "mas estables" de la entidad TCP son: Closed, Listen, Established. Los demas estados posibles son de transicion., ¿Cómo es el proceso de desconexión TCP?  → Desde el host que pide la desconexion, se envia un FIN, se recibe un ACK (cierra el flujo saliente). Luego se recibe un FIN y se envia un ACK (cierra el flujo entrante),
¿En qué estado debe estar la entidad TCP para intercambiar datos en dúplex completo? → En Established la entidad TCP puede intercambiar datos, tanto salientes como entrantes., ¿Por qué TCP es un protocolo orientado a la conexión? → Para poder hacer el control de secuencia, e implementar el ARQ sliding window, el TCP debe ser orientado a la conexion.,

¿Qué parámetros iniciales se configuran durante el establecimiento de la conexión? → Se setean el SN, el AN, el W y el MSS de cada flujo., Como es la transmision full-duplex? → En cada conexion TCP se transmiten 2 flujos independientes entre si, cada entidad tcp tiene un Tx y un Rx.,

En un segmento TCP transmitido, ¿qué campos del encabezado corresponden al flujo saliente y qué campos corresponden al flujo entrante? → Los Datos y el SN corresponden al flujo saliente. El AN, el ACK, y W, enviados en "piggyback", corresponden al flujo entrante., ¿Cómo es el proceso de conexión TCP? ¿Cuántos segmentos se necesitan? → La conexion TCP se establece mediante un "3 way handshake": desde el host que pide la conexion, se envia un SYN, se recibe un SYN+ACK, y se envia un ACK.,

¿Qué flags de control se utilizan en la conexion y en la desconexion? → SYN & ACK en la conexion, y FIN & ACK en la desconexion.
# 5
Respuesta parcialmente correcta.
Ha seleccionado correctamente 9.
La respuesta correcta es:
¿Qué pasaría si el RTO fuera mucho más alto que el RTT? → Si el RTO fuera demasiado largo se produciría una subutilización del canal.,

¿Cuáles son los parámetros ARQ que son variables y se adaptan dinámicamente? → En el ARQ de TCP, los parametros RTO y W (de cada flujo), son variables y se adaptan dinamicamente al estado de la red (en terminos de delay) y del estado de los buffers de recepcion en cada extremo., ¿Cómo se hace el control de errores? → La entidad TCP Tx envia los Datos con un SN. La entidad TCP Rx, si recibe los datos sin error, envia un ACK con un AN que indica el proximo byte que espera recibir. Si el Tx no recibe el Ack antes que se venza el RTO, retransmite los datos.,

¿Qué es el RTO? → El RTO, Retransmission TimeOut, es el tiempo que debe esperar el Tx antes de retransmitir los datos si no recibe el ACK correspondiente., ¿Cuál es el campo del encabezado TCP que se usa para secuenciar los datos recibidos en el Rx? → Gracias al SN, la entidad TCP receptora puede ordenar los datos en el buffer de recepcion aunque los datos lleguen fuera de secuencia o duplicados.,

¿Para qué se utiliza el checksum? ¿En qué casos es útil? → CheckSum sirve para el chequeo de la integridad del header y de los datos. Es util para el caso en que el segmento llega a destino pero alterado., ¿Qué indica el SN, el número de secuencia del segmento o el número de secuencia del primer octeto contenido en el segmento? → El SN indica el número de secuencia del primer octeto contenido en el segmento.,

¿Qué pasaría si el RTO fuera igual o menor que el RTT? → Si el RTO fuera demasiado corto se producirían retransmisiones inútiles., ¿Qué le puede pasar a un segmento TCP enviado por la red IP? → Los Segmentos TCP, en el transito por la red, pueden ser descartados y no llegar a destino, o llegar a destino alterados, o llegar duplicados, o llegar fuera de secuencia.,

¿Como es el algoritmo con el que el Tx calcula el RTO en base al RTT medido? → R(n),

¿En base a qué se ajusta dinámicamente el RTO? → El RTO se calcula en base al RTT Round Trip Time medido por el Tx.,

¿Qué significa AN? ¿Qué indica AN? → El AN es el Acknowledge Number. Indica el proximo byte que el Rx espera recibir, confirmando asi los bytes anteriores a AN.
# 6 
Respuesta correcta
La respuesta correcta es: Si el Tx recibe un segmento con AN=1000 y W=10000, ¿cuáles son los números SN que podrá transmitir sin esperar nueva confirmación y ventana? → El Tx, al recibir un AN=1000 y una W=10000, sabe que puede transmitir los bytes entre AN y AN+W-1 o sea entre 1000 y 10999., ¿En que consiste el principio de la gestión de ventanas TCP? → Para hacer un mejor aprovechamiento del ancho de banda disponible del canal, se utiliza el mecanismo ARQ Sliding Window que permite enviar varios mensajes con datos sin recibir la correspondiente confirmacion de correcta recepcion., ¿Cómo se puede calcular el throughput máximo en función del tamaño de la ventana y el RTT? → Siendo W la cantidad de bytes que se puede enviar, y siendo RTT el round trip time medido => Throughput = W / RTT, ¿Cuántos bits tiene la ventana de TCP? ¿Cuál es el tamaño máximo de una ventana? → La ventana W de TCP tiene 16 bits, o sea puede tener un tamaño maximo de 2^16 bytes (64KiB), Con un W de 16 bits (W<64kiB) y un RTT de 64ms, ¿cuál es el throughput (teorico) máximo que se puede lograr? → Con un W de 16 bits (W,
¿Qué significa el tamaño de la ventana? → El tamaño de ventana es la cantidad de datos (en bytes) que el Tx puede transmitir sin esperar a recibir el correspondiente Ack.

# 7

Respuesta parcialmente correcta.
Ha seleccionado correctamente 15.
La respuesta correcta es:
¿Qué es la Congestion Window (cwnd)? → La Congestion Window (cwnd) es la ventana que calcula el Tx para evitar sobrecargar la red. El Tx usa esta ventana cuando cwnd,

¿Cómo funciona el Tx para retransmitir más rápido un segmento perdido usando los ACK y ANs? → La deteccion de varios ACK duplicados (con el mismo AN) pone en evidencia que se perdio el segmento y por ende se puede retransmitir a partir del AN mucho antes que expire el RTO. Este mecanismo es llamado Fast Retransmit.,

¿Como se determina la cwnd con el algoritmo Congestion Avoidance? → Cada vez que recibe un ACK, el Transmisor Tx aumenta la cwnd = cwnd + 1/MSS,

¿Bajo qué condición el algoritmo de incremento de cwnd cambia de crecimiento exponencial a crecimiento lineal? → El algoritmo de incremento de cwnd cambia de Slow Start a Congestion Avoidance cuando cwnd>=SSThresh, ¿Cuál es la Advertized Window? ¿Qué representa la awnd del buffer de recepción? → La Advertised Window, awnd, es la W publicada por el Rx. Representa el espacio disponible del buffer de recepcion.,

¿Cómo crece la cwnd en la fase de Congestion Avoidance? → En la fase de Congestion Avoidance, la cwnd crece en forma lineal en funcion del tiempo (cwnd aumenta 1 MSS/RTT)., ¿Cuáles son los métodos para el control de sobrecarga de TCP? → El TCP implementa 2 métodos para el control de sobrecargas: el Control de Flujo y el Control de Congestión.,

¿Qué hace el Tx con el cwnd y el ssthreshold cuando detecta una pérdida de segmento debido a RTO (o sea, debido a congestion severa)? → Si se vence el RTO, el Tx retransmite los datos a partir de AN, setea ssthreshold a cwnd/2 y reduce la cwnd a 1MSS, Se dice que el control de flujo es explícito. ¿Por qué? → El Control de Flujo es explicito pues se basa en el uso de la Advertised Window, awnd, o sea la W publicada por el Rx.,

¿Qué cola evita sobrecargar el mecanismo de control de flujo? → El mecanismo de Control de Flujo es el que evita desbordar el buffer de recepcion del lado del TCP Rx., ¿Cuáles son las colas que se evita sobrecargar con el mecanismo de control de congestión? → El mecanismo de Control de Congestión evita desbordar las colas intermediarias que se forman en la red de packet switching (capa 3 y/o capa 2).,

¿Qué hace el Tx con cwnd y ssthreshold cuando detecta una pérdida de segmento debido a 3DupAck? → Si se detectan 3DupACK, ademas de retransmitir desde AN, el Tx retransmite los datos a partir de AN, setea ssthreshold a cwnd/2 y reduce la cwnd a ssthreshold. Es lo que se llama un Fast Recovery.,

¿Como se determina la cwnd con el algoritmo Slow Start? → Al inicio de la conexión TCP, el Transmisor Tx calcula la cwnd = 1MSS - Cada vez que recibe un ACK aumenta la cwnd = cwnd + 1 MSS,

¿Por qué la conexión tcp comienza con cwnd=1MSS? → Para evitar desbordar las colas intermediarias de la red, el Tx comienza con un pequeño tamaño de ventana cwnd=1MSS, y luego lo va incrementando a medida que recibe ACKs.,

¿Cómo crece la cwnd en la fase de Slow Start? → En la fase de Slow Start, la cwnd crece en forma exponencial en funcion del tiempo (la cwnd se duplica/rtt).,

¿En que se basan los métodos de FAST Retransmit y FAST Recovery? → Fast Retransmit y Fast Recovery se basan en la deteccion de varios ACK duplicados que ponen en evidencia que se perdio un segmento mucho antes que expire el RTO.,

¿Por qué el Tx, cuando detecta 3DupAck, reduce cwnd=ssthres en lugar de reducirlo a cwnd=1MSS? → En el Fast Recovery, el Tx reduce cwnd=ssthres (en lugar de reducirlo a cwnd=1MSS) pues asume que el segmento no fue descartado por congestion severa, por ende no es necesario reducir tan drasticamente la ventana de congestion., ¿Qué sucede cuando awnd=0? → Cuando la awnd=0 (la ventana W=0 publicada por el Rx) el Tx no puede seguir transmitiendo mas datos a partir del numero de secuencia AN.
