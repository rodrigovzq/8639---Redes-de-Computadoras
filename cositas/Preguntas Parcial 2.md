
# DNS

1. Explique sintéticamente que diferencia existe entre un servidor DNS primario y uno secundario. Cuántos puede haber de cada tipo? Ambos son autoritativos?
	Un servidor DNS es aquel que vincula nombres de dominio con direcciones IP. Un servidor primario es aquel que contiene toda la informacion acerca de un dominio, esto incluye zonas, IP, autoridades, identidad del dominio y quien es el administrador. Distinto es de un servidor DNS secundario, este tiene por objetivo mantener una copia actualizada del zone file que lo hace mediante una conectivdad con un servidor especial y este contiene el archivo en modo solo lectura para que el servidor primario pueda actualizarse. Ambos primario y secundario son autoritativos
2. Explique como funciona la resolución inversa en DNS. Que registros se involucran? Quien es responsable de administrar esa información?
	> La resolucion inversa se utiliza apra obtener el dominio de una direccion IP, para esto se usan los registros PTR en la zona de dominio especial in-addr.arpa. Estos PTR mapean direcciones IP a los nombres de dominio correspondientes, los servidores de dominio crean una relacion arbitraria mientras que  en el dominio in-addr.arpa si esta relacionado una conexion fisica
3. De un ejemplo de cómo se configura una delegación de zona research.mit.edu a partir de la zona mit.edu. Indique que registros se utilizan y cuáles son sus valores en el caso que research.mit.edu tenga 2 servidores DNS autoritativos.
a. En la zona *mit.edu* se debe crear un registro NS que indique a los servidores DNS autoritativos la subzona *research.mit.edu*

``` DNS
research.mit.edu IN NS ns1.research.mit.edu
research.mit.edu IN NS ns2.research.mit.edu
```
b. Luego se deben crear los registros A (address) para los servidores DNS autoritativos de la zona *mit.edu*. Estos asignan una direccion IP a cada servidor DNS autoritativo, por ejemplo
``` DNS
ns1.research.mit.edu IN A 192.0.2.1
ns2.research.mit.edu IN A 192.0.2.2
```
c. Con esta configuracion, la delegacion de zona de *research.mit.edu* se ha establecido a partir de la zona *mit.edu*. Los registros NS en la zona *mit.edu* indican los servidores DNS autoritativos para la subzona *research.mit.edu* mientras que los registros A en la zona *mit.edu* vinculan las IP de esos servidores DNS autoritativos

4. Suponga que el administrador de un server DNS primario para una cierta zona realiza cambios en la información de la zona pero olvida actualizar el número de serie del registro SOA.
a) ¿Qué problema se presenta?
	Sin la actualizacion del numero de serie del registro SOA, los aervidores DNS secundarios no tienen forma de saber si ha habido cambios en la zona y si necesitan solicitar una actualizacion por lo que no lo haran y habra inconsistencia de datos y proporcionarar respuestas incorrectas, ademas ed perder la redundancia y generar atrasos en las actualizaciones.
b) ¿Cómo puede percibir un cliente del DNS la situación?
	Puede percibirilo si un cliente DNS sabe que hay un cambio de IP a un servicio pero cuando escribe la direccion en un navegador, este le resuelve a la IP anterior
c) Si la zona tiene 4 servers autoritativos, ¿qué porcentaje de las consultas serán resueltas correctamente?
	Va a depender de la disponibilidad de los mismos y la estabilidad pero en promedio el 75% de las consultas deberian ser resueltas correctamente
5. Explique qué es el registro SOA, qué información contiene y cuál es su función.
	> El start of Authority es un tipo de registro en un sistema DNS que se utiliza para proporcionar informacion sobre una zona DNS. Este se encuentra como raiz de una zona y contiene informacion para la administracion
	> 	Nombre del servidor (Primary Name Server)
	> 	Email del administrador
	> 	Numero de serie: se usa para identificar actualizaciones en la zona
	> 	Refresh time: intervalo en que los servidores secundarios deben esperar para solicitar actualizacion
	> 	Retry time: Tiempo que deben esperar los secundarios para solicitar de nuevo una actualizacion de zona
	> 	Expiration time: tiempo maximo en que los secundarios pueden considerar valida su informacion almacenada
	> 	Minimum TTL: tiempo minimo que los registros de la zona pueden permanecer en cache


6. Cuándo una respuesta a una consulta DNS va a ser autoritativa? y cuándo
no sería autoritativa?
	La consulta es autoritativa cuando la respuesta venga de un servidor DNS que sea autoridad correspondiente al dominio solicitado. Autoritativa significa que el servidor tiene conocimiento directo, y esto ocurre cuando el servidor es primario o secundario. No es autoritativa cuando no ocurre lo anterior
7. En que difiere un Servidor Autoritativo de un Servidor No Autoritativo para una determinada Zona?
	Difiera en su capacidad para responder consultas DNS sobre una zona, la diferencia es que un servidor no autoritativo no puede dar respuestas autoritativas.
8. En que difiere una consulta Iterativa de una Recursiva?
	En una consulta iterativa, el cliente espera una respuesta parcial con una referencia para completar su consulta en otro servidor, asi sucesivamente hasta que tiene la informacion completa. 
	En una consulta recursiva, el cliente envia la solicitud y siempre espera una respuesta completa. Es el servidor el que se encarga de obtener la informacion realizando consultas a otros servidores.
9. De dónde obtienen la información que brindan cada uno de estos servers?
	DNS server primario: configurada y mantenida periodicamente por los administradores
	DNS server secundario: del DNS primario
	DNS server caching-only: de DNS autoritativo, primario o secundario
10. Enumere los tipos de registros RR y describa sintéticamente la función de cada uno de ellos.
	1. A (Address): Mapea un nombre de dominio a una dirección IPv4.
	2. AAAA (IPv6 Address): Mapea un nombre de dominio a una dirección IPv6.
	3. CNAME (Canonical Name): Mapea un nombre de dominio a otro nombre de dominio canónico. Se utiliza para establecer alias o nombres alternativos para un dominio
	4. MX (Mail Exchange): Especifica los servidores de correo (mail exchangers) que son responsables de recibir y procesar los correos electrónicos enviados a un dominio.
	5. NS (Name Server): Indica los servidores de nombres de dominio (DNS) autoritativos para un dominio. Proporciona información sobre los servidores responsables de mantener y servir la información de la zona.
	6. PTR (Pointer): Realiza la resolución inversa de direcciones IP a nombres de dominio. Mapea una dirección IP a un nombre de dominio.
	7. SOA (Start of Authority): Define parámetros de configuración y administración para una zona. Contiene información sobre el servidor DNS primario y otros detalles de la zona.
	8. TXT (Text): Almacena datos de texto libre asociados a un nombre de dominio. Se utiliza para diversos propósitos, como registrar información adicional, políticas de seguridad, entre otros.
11. Cual es la diferencia entre Zona y Dominio DNS?
	Una Zona es una porcion administrativa dentro de un dominio, una zona puede incluir a un dominio o una parte de él. 
	Mientras que un dominio DNS es una etiqueta o nombre utilizador para identificar una jerarquia  del sistema DNS.
12. Cómo podría el sistema de DNS facilitar la distribución de carga de un sitio Web? Desarrolle.
	Hay distintos metodos para distribuir la carga.
	- Round Robin DNS: mediante la distribucion de multiples registros RR con la misma prioridad pero condiferentes direcciones IP para el mismo nombre de dominio. Cada vez que se realice una solicitud, se va a responder con una IP distinta
	- DNS basado en ubicacion: usando DNS geograficos se puede determinar la ubicacion del cliente y  redirigirlo al servidor web mas cercano
	- DNS basado en carga: Algunos servidores pueden monitorear su estado y ajustar respuestas en funcion de ello
13. Qué significa que la resolución inversa una IP sea consistente (Forward-confirmed reverse DNS)? De un ejemplo de situación en la que se podría romper la consistentcia y qué buena práctica recomendaría?. Qué problemas podría traer que haya inconsistencia?
	FCrDNS es cuando la asociacion inversa es igual a la asociacion directa.
	Una sitacion donde puede ocurrir esta inconsistencia es cuando no se configuro bien la relacion entre IP y nombre de dominio.
	Uno de los problemas que podria traer es errores al enviar mails ya que el protocolo de mail realizan comprobaciones de FCrDNS para reducir el spam.

# Routing Protocols
1. Para cada uno de los Protocolos de Ruteo, indicar si es un Interior o Exterior GP, si usa Vector-Distance (hop-count)  o LinkState (Dikstra = costo), si propaga las rutas con netmask o no, si es abierto o propietario.

|       | IGP o EGP | VDS o LS | Netmask? |  Standard? |
|-------|-----------|----------|----------|------------|
| RIP   |     IGP   |   VDS    |    NO    |    OPEN    |
| RIP2  |     IGP   |   VDS    |    SI    |    OPEN    |
| OSPF  |     IGP   |   LS     |    SI    |    OPEN    |
| EIGRP |     IGP   |  LS+VDS  |    SI    | CISCO/OPEN |
| BGP   |     EGP   |   VDS    |    SI    |    OPEN    |


2. Desarrolle
a) Desarrolle al menos 3 ventajas de Rip versíon 2 respecto de Rip Versíon 1
- Propaga las Netmask de las rutas y entonces soporta VLSM y CIDR
- Soporta mecanismo simple de autenticacion
- Reducen la latencia en la propagacion de cambios en la topologia de la red con triggered updates
b) Desarrolle al menos 2 ventajas de los protocolos Link State respecto de
los Distance Vector
- Escalan mejor
- Convergencia mas rapida
3. Qué es un sistema autónomo, en el contexto de los problemas de ruteo?
- Una computadora que puede rutear utilizando tablas configuradas estáticamente
- **Un conjunto de redes y routers bajo una única administracíon que mantiene consistente el ruteo interno.** 
- Una interred separada de la Internet
> Un AS es un conjunto de redes que se encuentra bajo el control y la admnistracion de una organizacion. El proposito de un sistema autonomo es mantener un ruteo interno consistente dentro de su propia red. Un AS puede formar parte de internet

4. Cuáles son las diferencias entre los algoritmos de ruteo Vector Distance y los del tipo Link State? Realice una comparacíon entre ambos y de al menos un ejemplo de un routing protocol de cada tipo.

Los algoritmos de distance vector intercambian informacion entre sus vecinos directos, cada router tiene una vision limitada de la red y solo conoce las rutas y las metricas (que generalmente se basan en cantidad de saltos). Los routers actualizan y propagan sus tablas de enrutamiento de manera periodica o cuando se producent cambios en la topologia
Los algoritmos de link-state son de estado de enlace y recopilan informacion completa sobre la topologia de la red. Cada router tiene una base de datos de ruteo que contiene informacion detallada de los enlaces y a partir de esta inforamcion cada router calcula las rutas optimas utilizando el algoritmo de SPF que se basa en el costo de cada enlace.
Ejemplos
- VDP: RIP es un protocolo de vector de distancia que ya no se encuentra muy en uso pero si permanece legacy en empresas de telco
- LS: OSPF es un protoclo de estado de enlace comunmente utilizado que recopila informacion sobre la topologia de red y calcula las rutas mas cortas usando el algoritmo de SPF

# TFTP y FTP


1. FTP pasivo y FTP activo, en qué casos resulta conveniente cada uno?
**Modo Activo**
- El cliente origina una conexion desde un puerto efimero (N>1023) dirigida al puerto de control del servidor FTP (puerto 21)
- El servidor acepta la conexion
- El cliente escucha en el puerto N+1 y envia el comando por N+1 al servidor FTP
- *El servidor iniciara una conexion* contra el puerto N+1 indicado por el ciente usando el puerto 20 como origen
**Modo Pasivo**
- El cliente inicia la conexion sobre el puerto 21 del servidor FTP usando un puerto efimero N>1023
- El servidor repsonde con el comando PORT M (M>1023)
- *El cliente inicia otra conexion FTP* al puerto M indicado por el servidor
- Finalmente el servidor responde al puerto de datos del cliente

En general el metodo pasivo es el mas comun y recomendado en la mayoria de los casos ya que es compatible con una amplia gama de configuraciones de red, sin embargo puede haber ocasiones en los que el modo pasivo puede no funcionar por limitaciones de firewall y se pasa al uso del FTP activo

2. Si usted está construyendo un sistema embebido (y además debe programar-
lo), con un microprocesador no muy potente y necesita realizar transferencias de archivos no muy grandes, qué elegiría implementar TFTP o FTP? Por qué?

Elegiria TFTP porque este tiene muy bajo overhead en comparacion con FTP al usar el protocolo de transporte UDP que no esta basado en una conexion, para transferencias de archivos no muy grandes es conveniente ya que no es necesario mantener una conexion que verifique la integridad de la transferencia y certifique la recepcion de los mismos

# HTTP, Webservices

1. Qué diferencia hay entra URL y FQDN? Para acceder a un servidor web, la dirección debe comenzar con www.?
	Ambos estan relacionados con identificar y localizar recursos en internet pero un URL es una direccion que se utiliza para acceder a un recurso especifico en internet, la url consta de varios componenetes e incluye el procolo de comunicacion (http o https). 
	Por otro lado un FQDN es el nombre completo y unico de un dominio en internet. Consiste en el nombre de host y nombre de dominio separados por puntso. Un FQDN identifia de manera univoca a un recrusos en la jerarquia de nombres de dominio.
	No es necesario para acceder a una web que la direccion comience con www. ya que su uso con anterioridad era por convencion y no un requerimiento tecnico, esto es porque las entradas en las configuraciones DNS pueden ser personalizadas para permitir el acceso directo al dominio con y sin www.
	

2. Describa sintéticamente 3 diferencias entre http version 1.0 y version 1.1.
- 1.0 no tiene en cuenta completamente los asuntos de
	- proxies jerarquicos
	- caching
	- conexiones persistentes 
	- hosts virtuales (por agotamiento de IP)
- Multiples dominios pueden vivir en el mismo servidor 1.1


3. Se puede decir que HTTP tiene las siguientes características
- Genérico
- Stateless
- Orientado a Objetos
Explique el porqué de cada una

> Generico: Porque se puede usar para una amplia gama de aplicaciones y no esta limitado a un uso especifico
> Stateless: Es un protocolo sin estado, lo que significa que cada solicitud y respuesta son independientes entre si y no mantienen informacion de estado entre ellas
> Orientado a objetos: es un protocolo de capa de aplicacion utilizado para la transferencia de recursos y objetos dinamicos generados poraplicaciones web como resultados de consultas de bases de datos o contenido generado en tiempo real

4. Supongamos una página escrita en HTML:
``` HTML
< HTML >
< TITLE > BIENVENIDO A LA FIUBA </ TITLE >
< BODY BACKGROUND ="/images/back.gif " >
< H1 > FACULTAD DE INGENIERIA </ H1 > <P >
< IMG SRC ="/images/edificio.gif " > <P >
< A HREF =" http://www.cnn.com/forecast/" >
< IMG SRC =" http://www.cnn.com/images/cloudy.gif " > </ A > <P >
 <A HREF =" carreras.html " >
<IMG SRC ="/images/carreras.gif " > </ A > <P >
</ BODY >
</ HTML >
```
a) ¿Cuantas conexiones TCP utiliza el browser cliente (si usa HTTP 1.0)
en total para transferir la totalidad de la información desde el Server
WEB?
> Para el caso de http 1.0, se realiza una conexion TCP por cada elemento diferente que debe cargar la pagina, en este caso son 4
>	cargar /images/back.gif
>	carga /images/edificio.gif
>	carga http://www.cnn.com/images/cloudy.gif
>	cargar /images/carreras.gif


b) ¿Cual de los dos end-points (Browser ó Server Web) inicia cada una de
las conexiones?
> El navegador es el que inicia cada una de las conexiones dado que el enlace le llego de la primera conexion hacia la pagina web y debe solicitar el recurso asociado a la URL que la pagina indica

c) ¿Cómo indica el Server WEB que el objeto se transmitió completamen-
te?
> usando el campo Content-Length en la cabecera, este indica la longitud en bytes del cuerpo del mensaje y el cliente usa esta informacion para leer y recibir los bytes y saber cuantos esperar en la respuesta. Una vez que se han recibido todos los bytes esperados se considera que el objeto se ha transmitido completamente. De lo contrario la conexion se puede interrumpir o se agota el tiempo de espera. 

5. Qué protocolo de transporte usa el HTTP? En qué port (por default) escucha el server HTTP? 
	1. Describa la sintáxis del HTTP Request y del HTTP Response. 
	2. Describa el procedimiento con el cual probaría rápidamente que un servidor web está activo si dispone sólo del comando telnet.
> HTTP usa el protocolo TCP en el port 80 (escuchando) para las solicitudes no seguras y en el puerto 443 para las solicitudes HTTPS
> 1.
> 	HTTP REQ: 
> 		La linea inicial contiene el metodo HTTP (GET, POST, PUT, DELETE,etc) del recurso solicitado y la version HTTP utilizada
> 		Cabeceras: proporcionan la informacion adicional sobre la solicitod, como las cabeceras de autenticacion, contendio y control de cache
> 		cuerpo: solo presente en solicitudes que requieren enviar datos adicionales como en una solicitud POST
> 		`GET /data/new/index.html HTTP/1.0`
> 	HTTP RESPONSE
> 		La linea inicial contiene la version HTTP utilizada, cel codigo de estado y un mensaje descriptivo del estado
> 		Cabeceras: proporcionan info adicional de la respuesta como las de tipo contendio, longitud del contenido y las de control de cache
> 		cuerpo: opcional contiene el contenido real de la respuesta como el codigo HTML de una pagina web o el contenido de un archivo

``` html
HTTP/1.0 200 OK
Date: Fri, 31 Dec 1999 23:59:59 GMT
Content-Type: text/html
Content-Length: 1354

<html>
<body>
<h1> Feliza me muero </h1>
</body>
</html>
```

> 2. Si solo se posee el comando telnet se puede ejecutar contra el url y usando el puerto 80 o 443 segunn el tipo de conexion por ejemplo
> ` telnet google.com 80`


6. Describa la sintáxis de un URL genérico. Qué indica cada componente del URL? Aclare qué servicio de nombre se suele usar para resolver la asociación del hostname con la IP address?
> El formato completo de un URL generico es
> `<protocolo>://<host>:<port-number>/<path>`
> El servicio de nombre que se suele usar para resolver la asociacion es DNS
7. Describa la sintaxis de un mensaje HTTP request genérico. Como debe cambiar ese requerimiento si se utiliza un proxy HTTP?
> Un HTTP REQ generico es
> `<METHOD> <url> <http_version>`
> ejemplo : `GET /path/file.html HTTP/1.0`
> y un request cuando se utiliza un proxy requiere incluir el URL completo, no solamente el path, por ejemplo
> `GET http://www.somehost.com/path/file.html HTTP/1.0`

# MAIL

1. Para qué sirve y qué protocolo habla un Relay Mail Server?
> Relay mails erver es un servidor de retransmision de correo que sirve como intermediario en la entrega de email. Su principal funcion es recibir mensajes de un cliente o servidor y luego retransmitirlos al destinatario final. El protoclo que usa esto es SMTP (Simple Mail Transfer Protocol)

2. Qué se realizó para permitir el envió de archivos binarios y caracteres especiales por e-mail?
	El lanzamiento del estandar MIME soluciona esta limitacion heredada de SMTP, ademas tiene la posibilidad de enviar elementos como imagenes o audio, etc. En la cabecera de MIME se especifica el tipo y la codificacion del adjutno asi que eso permite que el receptor lo interprete adecuadamente
3. Compare
	 a) POP3 e IMAP4
	 Ambos son protocolos utilizados para acceder a correos en servidores remotos
	 - **POP3** (Post office protocol 3): 
		 - descarga los correos desde el servidor hacie el dispositivo y los elimina del servidor. El usuario accede a una copia local de sus mensajes y no puede realizar acciones sobre los mensajes almacenados en el servidor. 
		 - No mantiene sincronizacion entre dispositivos
	 - **IMAP4** (Internet message access protocol): 
		 - Tambien descarga los correos pero mantiene la copia en el servidor, permitiendo al usuario hacer cambios y administrar los mensajes en el dispositivo y el servidor. 
		 - mantiene sincronizacion entre dispositivos 
4. Describa sintéticamente cómo es el proceso y cuáles son los protocolos involucrados en cada transacción para que un usuario@dominio1.com pueda enviarle un mensaje a un destinatario@dominio2.com.ar
> Composicion del mensaje: usuario@dominio1.com redacta el mensaje en su cliente de mail, incluyendo el remitente, el destinatario y asunto
> SMTP: una vez que el mensaje esta listo para ser enviado, se utiliza este protocolo para establecer conexion con el sercidor de correo saliente SMTP del dominio1.com. El cliente envia el mensaje a ese servidor.
> Enrutamiento del mensaje: el servidor SMTP del dominio1.com utiliza el sistema DN para buscar lso registros MX del dominio2.com.ar. Estos registros indican los servidores de correo  entrante SMTP para dominio2.com.ar
> Transferencia del mensaje: El servidor del que envia se conecta con el del receptor utilizando TCP/IP. El servidor del remitente encia el mensaje a traves de esta conexion.
> Almacenamiento y entrega: el servidor SMTP del detinatario recibe el mensaje y lo almacena en su cola de correo entrante. Luego el protocolo POP3 o IMAP4 son los encargados de entregar el mensaje al dispositivo que usa el destinatario
> Descarga del mensaje: El cliente de correo del destinatario coenctado al servidor de correo dominio2.com.ar descarga el mensaje usando pop3 o imap4 y este puede leer el mensaje en su cliente de correo electronico 

5. Describa sintéticamente la arquitectura y los protocolos involucrados en el sistema de mail estándar sobre IP
![[Pasted image 20230704213218.png]]
![[Pasted image 20230704213516.png]]
> La arquitectura1  
> 	consta de un Mailtool que es el cliente de mail que maneja el protocolo SMTP para conectarse a un Mailhost y enviar un correo
> 	El Mailhost utiliza el protocolo DNS para conocer la direccion IP del destinatario usando los registros MX y establecer conexion con el Mailserver.
> La arquitectura 2
> 	Consta del mail tool que usando pop o imap se conecta con un mailbox buscnaod correos nuevos, mientras que el mailbox recibe conexiones SMTP de un mailserver para recibir correos nuevos



6. Qué debe hacerse para que el usuario juan@cia.com.ar, cuando el server de mailbox donde está su cuenta esta conectado a la internet solo un rato por día, continúe pudiendo usar su address de e-mail normalmente?
	> debe usar la arquitectura de mailbox para tener sus correos alli hasta que se conecte y pueda descargarlos
	> o se configura  una direccion de redireccion de correo entrante hacia otra cuenta en la cual pueda tener acceso


7. Qué es SMTP? Describa el díalogo protocolar SMTP entre 2 MTAs.

Es un protoclo de red utlizado para la transferencia de correos electronicos entre servidores MTA (mail transfer agents)
	1. El MTA1 inicia una conexion TCP con el receptor MTA2 via TCP por puerto 25
	2. MTA1 envia comando `HELO` seguido de su nombre de dominio
		1. `HELO example.com`
	3. MTA2 responde con un codigo generalmente `250 OK`
	4. MTA1 envia el comando `MAIL FROM` seguido de la direccion del remitente
		1. `MAIL FROM mutard@fi.uba.ar`
	5. MTA2 responde con un codigo de respuesta indicando si el remitente es aceptado
	6. MTA1 envia el comando `RCPT TO ` seguido de la direccion del destinatario
		1. `RCPT TO nmatsunaga@fi.uba.ar`
	7. MTA2 responde con un codigo indicando si valida
		1. Este proceso se repite por cada RCPT TO
	8. MTA1 envia el comando `DATA` para indicar que comenzara a enviar el contendio del mensaje
	9. MTA1 Envia el mensaje con encabezado y cuerpo
	10. MTA1 finaliza el mensaje enviando un punto en una linea separada
	11. MTA2 responde con un codigo de respuesta validando si el mensaje fue entregado correctamente
	12. MTA1 envia comando `QUIT` 
	13. MTA2 responde con codigo de respuesta y cierra la conexion TCP

# SNMP

1. Enumere las operaciones posibles en SNMP versión 2, indicando para cada caso la entidad (nms o agent) que la puede generar y las PDUs asociadas.
	1. `get`: para tomar el valor de una variable MIB. 
	2. `set`: para modificar el valor de una variable MIB
	3. `get_next`: para para tomar el valor de una variable MIB pero en modo de acceso *transversal*. Toma el siguitente OID en la secuencia
	4. `get_response` para devolver el valor de una variable MIB. esta es generada solo por el agente
	5. `trap`: reportar eventos extraordinarios, esta es generada solo por el agente
2. Qué es y para que se usa SMI1? Qué es una MIB2 y cómo se identifican los objetos en SNMP
	1. SMI: Structure of Management Information es una especificacion para definir y organizar la informacion de gestion en un formato estandarizado. Establece reglas basicas para la definicion de los objetos gestionados y sus OID
	2. MIB2 : Management information base es un estandar definido en SNMP, es una coleccion de objetos gestionados que representan informacion de gestion comunmente utilizada en dispositivos de red.
	3. Los objetos gestionados son llamados OID, estos permiten identificar de manera unica cada objeto en la MIB. Los OID se componene de una serie de numeros separados por puntos, cada numero representa un nodo en la jerarquia de objetos


3. Qué tipo de variables existen en SNMP? Cómo se recorre la información en las tablas? (por ej, la dibujada a continuación) Qué PDU utilizaría una aplicación que “baja” esta información?
	![[Pasted image 20230704202940.png]]
La informacion se recorre de arriba hacia abajo  y de izquierda a derecha  la pdu que se utiliza es get_next

```
|       |       |       |       |
|       |       |       |       |
|       |       |       |       |
|       |       |       |       |
|       |       |       |       |
↓       ↓       ↓       ↓       ↓
```

De la rama interfaces  ::{mib-2 2} 1.3.6.1.2.1.2
se tienen las siguientes variables

	1. ifNumber
	2. ifTable
		1. ifEntry
			1. ifIndex
			2. ifDescr
			3. ifType
			4. ifMTU
			5. ifSpeed
			6. ifPhysAddress
			7. ifAdminStatus
			8. ifOperStatus
			9. ifLastChange
			10. ifInOctets
			11. ifInUcastPkts
			12. ifInNUcastPkts
			13. IfInDiscards

4. Qué significan las siglas SNMP y cuál es la función del mismo (por qué se lo necesita)?
	Simple Network Managment Protocol sirve para gestionar y supervisar dispositivos en una red, como routers, switches, servidores y otros dispositivos de red. Su objetivo principal es permitir la administracion centralizada y el monitore de estos equipos desde un sistema de gestion de red NMS (Network management system)
	
5. Qué tipo de información se administra mediante SNMP?. ¿Como se llama al conjunto de elementos que la componen, en que formato se la representa, como se organiza para un fácil direccionamiento de los mismos?
	El tipo de informacion que se administra en SNMP puede ser configuracion, kpis de rendimiento,estado de servicios y aplicaciones e informacion de seguridad.
	El conjunto de elementos que la componene se llama MIB y represetna una estructura jerarquica de los objetos que seran gestionados, donde cada objeto representa una propiedad y es identificado con un OID. El MIB es un archivo de texto llamado SMI (structura of management information), alli se definen las reglas y las convenciones para describir a los objetos y su relacion con la sintaxis

6. ¿De qué maneras puede una plataforma de network management enterarse de eventuales cambios en el contenido de la información del dispositivo a administrar?
	Mediante el metodo de polling con solicitudes GEt o bien con la operacion TRAP que venga de un agente

7. ¿Como funciona la validación de operaciones entre agentes y estaciones de gestión?. ¿Cuál es su principal falencia de seguridad?. ¿Que propondría Ud. Para resolverlo?.
	La validacion se realiza mediante un proceso de autenticacion de la comunidad y autorizacion. Una vez autenticado, el gestor SNMP envia solicitudes de operacion y SNMP verifica los permisos y los roles asignados. La falencia es el tipo de autenticacion de la comunidad, la comunidad SNMP es una cadena de texto que actua como una contrasena para acceder al agente, este verifica si la comunidad suministrada coincide con la configurada 
	Como propuesta para mejorar esto propondira un sistema de autenticacion nativo con usuario y contrasena elegible por el gestor

8. Justifique por que razón el protocolo SNMP funciona sobre UDP en lugar de utilizar TCP.
	1. Eficiencia y velocidad ya que es un protcolo muy liviano, al ser compatible con una gran gama de dispositivos, algunos muy acotados en velocidad de enlace
	2. Naturaleza sin estado: SNMP es un protocolo sin estaod lo que significa que cada solicitud se puede considerar independeinte y no requiere mantener una conexion persistente. UDP seria el protocolo mas apropiado para esta caracteristica
	3. Flexibilidad y escalabilidad: UDP permite la transmision de manera no secuencial y sin garantia de entrega, lo que proporciona flexibilidad y escalabilidad en entornos de red ya que los paquetes SNMP pueden enviarse y recibir en cualquier orden sin restricciones secuenciales

# QoS, VoIP

1. QOS & VoIP. ¿Qué es el delay jitter ?
	El delay jitter es la variacion que hay en el delay de la comunicacion, esto es cuando los paquetes de datos tienen fluctuaciones en el tiempo de entrega debido a congestiones, problemas de enruatamiento o cuellos de botella en la red
2. ¿Por qué es más negativo para el tráfico de VoIP que para el tráfico de HTTP? 
	Porque la naturaleza del trafico VoIP es de datos en tiempo real, el delay jitter provoca desincronizacion entre los paquetes de voz por lo que afecta la fluidez y la comprension de lo que se este conversando. Para HTTP se tiene transferencia de datos que no es critico una comunicacion en tiempo real de manera que se vea gravemente afectada por una variacion en el delay que tenga actualmente esa comunicacion.

3. ¿Qué mecanismo debe implementarse en el receptor para compensar el delay jitter y permitir la correcta reproducción de audio?
	El receptor puede incorporar un mecanismo de buffering, esto es almacenar temporalmente alggunos paquetes de audio y retenerlos de manera de que cuando exista una extension muy pronunciada del delay promedio, se vayan liberando y entregando los paquetes almacenados en el buffer para dar la impresion al usuario receptor de que la comunicacion continua normalmente y asi compensar los efectos del delay jitter.


# Seguridad

1. Cómo se puede firmar digitalmente un documento ?
- Cifrando el mensaje.
- Cifrando un hash de su contenido con la clave pública del destinatario
**- Cifrando un hash de su contenido con la clave privada del remitente**
	Una forma es un cifrado del contenido mediante el mecanismo asimetrico de calve publica y clave privada. La clave privada se usa para cifrar y la publica para decifrar, entonces un mensaje cifrado por un remitente con su clave privada se puede considerar firmado ya que solo el tiene acceso a esa clave y se puede verificar decifrando el mensaje con la clave publica que el remitente compartio y solamente con esa

2. ¿Qué diferencia hay entre un firewall que funcione filtrando paquetes sin memoria (sin historia, o sin seguimiento de estado) o con ella? Para qué sirve la inspección con memoria o seguimiento de estado (stateful inspection)?
	La diferencia es que un firewall con memoria permite hacer el stateful inspection. Un fw sin memoria permite hacer un filtrado de paquetes de forma individual y aplica reglas de filtrado en funcion de la informacion que contiene cada paquete. Este fw no mantiene informacion sobre el **estado** de las conexiones
	Un FW con memoria utiliza tecnicas de inspeccion que le permiten comprende el contexto y el estado de las conexiones lo que brinda la capacidad de tomar decisiones mas sofisticadas que en el caso anterior, como permitir trafico entrante que corresponda a una conexion establecida o bloquear paquetes que no se ajsten a un estado esperado. Este tipo de inspeccion proporciona una mayor seguridad porque permite filtrar ataques mas sofisticados como intentos de eludir fw con tecnicas de fragmentacion de paquetes

3. Explique y realice un diagrama del proceso de validación de la firma digital de un mensaje M. ¿Qué servicio de seguridad no provee la firma digital? ¿Qué es un certificado de clave pública, y cual es su utilidad?
![[Pasted image 20230705185257.png]]

La validacion del proceso de un mensaj M con firma digital es mediante la transferencia de la clave publica hacia el destinatario, esto se puede realizar mediante el algoritmo de Diffie Hellman. Luego el destinatario recibe el mensaje cifrado y con la clave publica podra decifrarlo y leer el mensaje. La verificacion existe porque la transferencia de la clave publica la realizo el emisor del mensaje y la validacion es porque solo con ella se puede decifrar el cipher enviado.
Los servicios que no poseen PKI son SSH y SNMP

4. Explique el principio de funcionamiento de los siguientes elementos criptográficos. Para cada uno de los servicios de seguridad, que elementos se requiere?
- Hash
	- es una funcion matematica que distribuye uniformemente los mensajes que toma como argumento sobre un espacio de imagen acotado pero lo mas grande posible. La idea de un hash es ocultar el contenido de un mensaje y que sea muy liviano computacionalmente de ejecutar pero muy dificil de hacer en reversa. De esta manera se puede proteger informacion y brindar privacidad con un costo computacional no muy alto
- Cifrado simétrico
	- Es un metodo de proteccion de datos que consiste en codificar un mensaje utilizando una clave como semilla del algoritmo de cifrado de tal manera que cambiando la clave, cambie el cifrado. La propiedad de simetria la brinda el utilizar la misma clave tanto para cifrar como para decifrar
- Cifrado asimétrico
	- El cifrado asimetrico tiene como diferencia que la clave para cifrar es distinta que la clave para decifrar, llamadas clave privada y clave publica respectivamente. Este metodo es mas seguro que el anterior al no tener la necesidad de comunicar la clave con la que se realiza el cifrado, de esta forma agotando un punto debil que tiene el metodo anterior. Aunque como contrapartida posee que normalmente es mas lento el cifrado asimetrico


5. En un firewall alguien coloca una única regla: Se impide el paso de paquetes TCP entrantes al perímetro protegido, si tienen en 1 el bit de SYN y en 0 el bit de ACK al mismo tiempo. ¿Qué efecto tiene esta regla?
	Si envia un SYN en 1 y ACK 0 es que tiene intension de conectarsem entonces al ser una conexion entrante via TCP, sera bloqueada si es una conexion nueva. No asi para conexiones ya establecidas, porque el SYN sera mayor y el ACK tambien

6. Por qué se utiliza un sistema simétrico junto con uno de clave pública ?
- Porque el de clave pública no sirve para encriptar.
- **Porque no es sencillo distribuir la clave en el simétrico.**
- Porque el de clave pública es muy lento cifrando
> Se utiliza este metodo hibrido y el sistema asimetrico se utiliza para la distribucion de la unica clave del sistema simetrico dado la sensibilidad de esta informacion y la necesidad de encontrar un canal seguro para esta transferencia


7. Cómo se puede asegurar que sólo el destinatario conozca el contenido de un mensaje ?
- Cifrando su contenido con la clave pública del destinatario .
- **Cifrando su contenido con la clave privada del remitente**
- Calculando un hash del mensaje y transmitiéndolo.
> Cifrando con Sk se puede asegurar que solo el destinatario conozca el detino del mensaje si el solamente posee la clave publica del emiso

8. Ud. desea permitir las consultas al WWW originadas en la internet y dirigidas a un server ubicado detrás de un firewall. Especifique las reglas a instalar en la interfaz externa del firewall para permitir el funcionamiento correcto del sistema. Ej: Regla: Protocolo=TCP; Dirección=entrante; PortTCP=80; Acción=PERMITIR
```
Protocolo=TCP; Dirección=entrante; PortTCP=80; Acción=PERMITIR
Protocolo=TCP; Dirección=entrante; PortTCP=443; Acción=PERMITIR
Protocolo=UDP; Dirección=entrante; PortUDP=53; Acción=PERMITIR
```


9. Sea un datagrama de tamaño 1500 Bytes, que transporta un segmento TCP correspondiente a una conexión del WWW dirigida al server interno A. En el curso de su transito a través de la internet, el datagrama es fragmentado en 3 partes del mismo tamaño aproximadamente. Posteriormente los fragmentos deben atravesar un firewall sin memoria. Indique qué sucede con cada uno de los 3 fragmentos en los siguientes casos:
	a) Si en el firewall se coloca una regla que bloquee el tráfico de IP dirigido al server A
		**DENIED**
	b) Si en el firewall se coloca una regla que bloquee el tráfico de TCP
	dirigido al port 80 de cualquier server interno
		**DENIED**
	c) idem a) pero el firewall tiene funcionalidad de reensamble de datagramas previo al filtrado.
		**DENIED EL ENSAMBLADO**
	d ) idem b) pero el firewall tiene funcionalidad de reensamble de datagramas previo al filtrado.
		**DENIED EL ENSAMBLADO**