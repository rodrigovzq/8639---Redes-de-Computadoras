- ¿Conoce el Sistema de Nombres de Dominio (DNS) y puede explicar cómo funciona?
	- Asocia nombres con IP, nombres con nombres
	- Full qualified domain name
		- prefijo y sufijo
	- Alias/canonical name

- ¿Por qué surge la necesidad del protocolo DNS?
	- Porque nos acordamos de los nombres y no de los numeros

- ¿Qué se entiende por resolución de nombres en DNS?
![[Pasted image 20230515174546.png]]


- ¿Qué es un FQDN? - ¿Cómo está estructurado?
	- Full qualified domain name
	- secuencia de labels separados por puntos
	- Ejemplo fi.uba.ar
	- 63 caracteres como maximo cada etiqueta
		- packet string: porque el primer octeto refleja la longitud del string
		


- ¿Cuál es el FQDN del servidor web de la FIUBA? - ¿Y la URL?
	- fi.uba.ar FQDN
	- https://fi.uba.ar URL

- ¿Cuántos caracteres puede tener cada etiqueta FQDN?
	- 63 por etiqueta

- ¿Cómo usar el comando nslookup para averiguar la dirección IP asociada con el FQDN del servidor web de la FIUBA?
![[Pasted image 20230515175006.png]]


- ¿Cómo se llama el proceso del cliente DNS?
	- DNS Resolver

- ¿Cuáles son los datos indicados por el Resolver en una consulta DNS de una búsqueda de direcciones (resolucion directa)? - ¿Cuáles son los datos que el Resolver espera recibir en la respuesta DNS?
	- Espera recibir el FQD y devuelve el registro de la tabla DNS. La asociacion
	- 

- ¿Cuál es la diferencia entre los conceptos de dominio y zona?
	- ARBOL LEXICOGRAFICO: se lee de derecha a izquierda
		- define nombre de forma univoca
		- delega autoridades
		- 
	- FQDN se compone por nombre de host y nombre de dominio
	- *hostname.subdomain.domain.**topleveldomain***
		- topleveldomain: ar
		- domain: uba
		- subdomain: fi
	- TLD: suelen ser los de los paises
- ¿Cuál es la relación entre los conceptos de zona, entidad administrativa y autoridad?
	- Dominio: la totalidad de los nodos descendientes de un cierto nodo (un sub-árbol)
	- Zona: una porción de un dominio, administrada por una entidad administradora. Los límites de las zonas están establecidos por la forma con que se particiona y distribuye la autoridad sobre la base de datos distribuida.
	- ![[Pasted image 20230515180016.png]]
	- ![[Pasted image 20230515180036.png]]
	- ![[Pasted image 20230515180313.png]]
	- Un query recursivo y multiples queries recursivos

- ¿En qué protocolo de transporte se ejecuta el DNS? - ¿Qué números de puerto están reservados para DNS?

- ¿Cuáles son los diferentes tipos de servidores de nombres?


- ¿Cuál es la diferencia entre los servidores de nombres autorizados para una zona y los NS no autorizados?

- ¿Cuál es la diferencia entre el servidor primario y los servidores secundarios en una zona?
	- Primario: el admin modifica los registros
	- Secundarios: se actualizan con la info del primario mediante el Zone Transfer. Se actualiza el SOA (star of authority)

- ¿Qué procesos DNS almacenan en caché las respuestas obtenidas? - ¿Por qué lo hacen?
	- Para evitar consultas muy seguidas
	- El tiempo de vida lo settea el administrador

- ¿Cuánto tiempo se puede almacenar un RR en un caché de DNS? - ¿Quién lo define?
	- Lo define el administrador
	- se almacena el tiempo en un parametro que se llama TTL
	- TTL fiuba = 1min
	- TTL uba = 2h

- ¿Podría distinguir la resolución de nombres recursiva e iterativa en DNS?
	- 

- ¿Qué tipo de resolución no es soportada por los servidores de Root Level?
	- 

- ¿Cuál de los tipos de resolución genera la mayor sobrecarga para un servidor de nombres?
	- La recursiva

- ¿Qué son los RR? - ¿Cuáles son los diferentes tipos de RR?
	- Resourse Record
	- Indice: FQD
	- tiene TYPE, CLASS, TTL, RDLENGTH,
	- Me indican que parte del registro responde la query

- ¿Qué tipo de RR se solicita al realizar la búsqueda directa de direcciones?

- ¿Qué información proporcionan los RR de tipo NS?

- ¿Para qué se utiliza el RR SOA? - ¿Qué información contiene?
	- elTTL del cache

- ¿Qué es la delegación de autoridad de una zona padre a una zona hija?
	- La hija pega glue records que la zona padre no tiene autoridad
	- se utilizan en el padre para indicar el address de IP de los nameservers autoritativos para la zona hija. Sólo son necesarios si el nombre de éstos está dentro de la zona hija (evitan el problema de la dependencia circular)
	- ![[Pasted image 20230515183808.png]]

- ¿Cuándo ocurre una lame delegation (delegacion "renga")?
	- cuando un server delega sobre otro pero este no ha sido configurado 
	- problemas de performance
	- Ocurre cuando un server delega en otro autoridad sobre una zona, pero éste no ha sido configurado como autoritativo para esa zona (o esta fuera de servicio).
	- Se genera tráfico innecesario sobre la internet, y demoras debido a las consultas no respondidas hechas a los lame servers.
	- Se compromete la disponibilidad debido a una falsa percepción de redundancia.

- ¿Para qué se utiliza la búsqueda inversa de direcciones?

- ¿Qué tipo de RR se solicita al realizar una búsqueda inversa de direcciones?
	- PTR

- ¿Para qué sirve la transferencia de zona? - ¿Cómo se utiliza el RR SOA?
	- Se usa para sincronizar los secundarios con el primario

- ¿Cuál es la autoridad de registro de nombre a la que debe solicitar la delegación de una zona bajo .ar?
	- NIC.AR