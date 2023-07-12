
- ¿Cuál es la finalidad del servicio de mail?
	- Enviar mensajes a un destinatario, remitente, con un asunto
	- Mailtool es una herramienta que corre en un browser usualmente, pero se puede hostear de manera local

- ¿Cuáles son los componentes de la arquitectura del servicio de mail?
	- ![[Pasted image 20230529172215.png]]

- ¿Qué protocolo es utilizado para el envío de mails?
	- SMTP

- ¿Qué protocolo de transporte utiliza el protocolo SMTP? - ¿En qué port escucha el mail server?
	- Trabaja sobre TCP en el puerto 25

- ¿Qué RFCs definen el envío de mails vía SMTP? - ¿Qué estandariza cada uno de ellos?

- ¿Cuáles son los mensajes intercambiados por el protocolo SMTP? 
	- Mensajes de respuestas para los comandos
	- ![[Pasted image 20230529174025.png]]

- ¿En cual de ellos se especifica el remitente del mail?
	- MAIL FROM:

- ¿En cual de ellos se especifica el destinatario del mail?
	- RCPT TO

- ¿Cuáles son las partes en las cuales se compone/descompone cada mensaje de mail?
	- ![[Pasted image 20230529174227.png]]
	- 

- ¿Cómo se conforma una dirección de mail? 
	- *nombredeusuario* **@** *dominio*

- ¿Qué diferencia hay entre una cuenta de mail, un alias de mail y una lista de distribución de mail?
	- El alias es una dirección que reenvía los correos a una cuenta de mail especifica
	- una lista es una dirección que reenvía los correos a un grupo de cuentas de mails

- ¿Qué diferencia hay entre una dirección de mail, un URL y un FQDN?
	- direccion de mail: usuario@dominio
		- el dominio es un FQDN
	- url: https://FQDN/path

- ¿Qué estándar se usa para el envío de mensajes en formato multimedia?

- ¿Para que se usan los registros MX de DNS? - ¿Cómo se usan?
	- Se usan para obtener la IP del destinatario
	- Ejemplo:
		fsc5.stn.mlv.fr
				IN MX 0 fsc5.stn.mlv.fr.
				IN MX 2 psfred.stn.mlv.fr. 
				IN MX 4 mvs.stn.mlv.fr.

- ¿Qué protocolos pueden ser utilizados para acceder a los mails de una cuenta en un mailbox server?

- ¿Qué protocolo de transporte utiliza el protocolo POP y el IMAP? - ¿En qué ports escucha el MailBox Server?

- ¿Qué diferencia funcional hay entre el protocolo POP y el IMAP?

- ¿Para que se usan los registros TXT SPF de DNS? - ¿Cómo se usan?

