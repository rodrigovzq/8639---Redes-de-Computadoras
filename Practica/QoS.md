# Quality of Service

- El proveedor de internet usa esto para limitar mi velocidad
	- Traffic shaping
- aplicacion tipica en VoIP
- Integrated services vs Differenciated services
- **Packet switching impairments**
	- Packet Loss
		- en medios wireless es comun
	- Delay
		- por tiempos de serializado, encolador
		- variacion del delay -> jitter
	- a mas trafico, mayor probabilidad de impairments, loss y delay
- Mecanismos de QoS
	- Priorizar el trafico
	- Reserva/garantia de ancho de banda
- Red Best Effor
	- red que no implementa QoS
- Best Effort sobredimensionada
	- Ofrece buena calidad de servicio pero a un costo alto
- Red QoS
	- ofrece buena calidad de servicio y es adaptado a los requerimientos del usuario
- Servicios integrados (IntSer)
	- implementa el enfoque parametrizado, usa protocolo RSVP de reservacion de recurso para solicitar y reservar recursos en la red
- Servicios Diferenciadios (DIFFSERV)
	- Implementa modelo priorizado, clasificacion de los paquetes en el header IP, en el bit de ToS
- PHB Classes
	- Default: best effort
	- Expedited: baja perdida y baja latencia
	- Assured: asegura la entrega del paquete

## BBR -> paper bottleneck rountrip time

- como varia el RTT con los inflight packets
- latencia en funcion de los inflight
- muestra como se corrige el aumento de lo anterior
- TCP cubic mejra pero no vacia la cola que queda en 100ms y como empeora de nuevo
- TCP BBR fija el valor maximo de la cong window gain y va estimando parametros de la red, como el bandwidht disponible y va corrigiendo bajando la latencia operando

## VoIP

