- ¿Cuales son las funciones de gestion (management) identificadas por la ISO con las siglas FCAPS?

- ¿Para qué sirve el protocolo SNMP?
	- Para gestionar aspectos de performance

- ¿Porqué es relevante que SNMP sea simple?
	- Para enfocar el agente en su tarea puntual


- ¿Como se denomina a cada entidad en el dialogo SNMP? - ¿Cual es la entidad que requiere información y cual la que la brinda? 
	- Manager requiere informacion
	- Agent brinda informacion
	- La interaccion es como la de cliente servidor pero cambia el vocabulario

- Enumere distintos Managed Nodes. - ¿Cuales de estos pueden ser sistemas abiertos y cuales no?
	- ![[Pasted image 20230529182934.png]]
	- Los que son abiertos pueden ser administrados

- ¿Qué se entiende por MIB? - ¿Qué diferencia hay entre una MIB Variable  y una MIB Definition?
	- Managed information based
	- Son las variables de administracion que manejan los agentes que representan aspectos de la configuracion
	- como una variable de interfaz que esta UP o DOWN

- ¿Porqué es impotante que tanto el protocolo SNMP como las MIB Definitions sean estandares abiertos?
	- Porque los desarrolladores del software del agente es distinto que los del manager entonces debe haber un estandar que los unifique

- ¿Cuáles son las operaciones soportadas por el protocolo SNMPv1?  
	- get
	- set
	- get_next
	- get_response
	- trap

- ¿Qué PDUs define el SNMP v1? - ¿Qué PDUs son utilizadas por cada operacion?
- ![[Pasted image 20230529183622.png]]

- ¿Qué es un OID? - ¿Qué estructura tiene el OID? - ¿Para qué se usa el OID?
	- Object ID
	- Sucesion de numeros para decodificar la indicacion de que quiero leer o escribir
	- iso 

- Describa el formato del mensaje SNMP.

- ¿Qué es el Community Name? - ¿Para qué se usa?

- ¿Qué es el ReqID? - ¿Para qué se usa?

- ¿Cuantas variables MIB pueden ser leidas o escritas en un mismo mensaje SNMP?

- ¿En qué campos del header SNMP se indican los errores? Enumere algunos ejemplos de errores posibles.

- ¿Qué significa que un SNMP Response tenga un Error de tipo "Too big"?



- ¿Qué lenguaje se utiliza para establecer una MIB Definition?

- ¿Qué types pueden ser especificados en el campo SINTAX de la definicion de una variable MIB?

- ¿Qué puede ser especificado en el campo STATUS de la definicion de un objeto MIB?

- ¿Qué puede ser especificado en el campo ACCESS de la definicion de un objeto MIB?



- ¿Qué se entiende por subtype? 

- ¿Que diferencia hay entre un OCTETSTRING y un DisplayString?

- ¿Que diferencia hay entre un OCTETSTRING y un IPAddress?



- ¿Para qué sirven los Traps?

- ¿Cuales son los posibles GenericTrapNumber?

Si el GenericTrapNumber=Specific - ¿Como se interpreta el EntrepriseID y el SpecificTapNumber?

- ¿Porqué el Trap especifica un AgentAddr?



- ¿En base a que parametros se puede establecer un control de acceso a un SNMP Agent?



- ¿Qué se entiende por variables MIB escalares y tabulares?

- ¿Cual es el numero de instancia que se utiliza en el OID para hacer un get o un set de una variable escalar?



- ¿Cuales son los MIB Groups definidos en la MIB Definition MIB-II?

Las variables definidas en el grupo System, - ¿son tabulares o escalares?



- ¿Qué informacion brinda la variable SysDescr?

- ¿Cual es el OID que se debe utilizar para hacer un get de la variable SysDescr?

- ¿Es posible hacer un set de la variable SysDescr?



- ¿Qué informacion brinda la variable SysName?

- ¿Cual es el OID que se debe utilizar para hacer un get de la variable SysName?

- ¿Es posible hacer un set de la variable SysName?



- ¿Qué informacion brinda la variable SysUpTime?

- ¿Cual es el OID que se debe utilizar para hacer un get de la variable SysUpTime?

- ¿Es posible hacer un set de la variable SysUpTime?



Las variables debajo de la rama ifTable - ¿son variables escalares o tabulares?

- ¿Que indica la variable escalar ifNumber?

- ¿Como se indexan las variables tabulares debajo de ifTable?

- ¿Como se recorre la tabla IfTable si se utiliza la operacion traversal (getnext&response)?

- ¿Que diferencia hay entre la variable ifOperStatus y la variable ifAdminStatus?

- ¿Que variable de la tabla ifTable describe la MAC address de la interface?

