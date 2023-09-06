### Ejercicio CiberKillChain - Ataque

## Alumno: Ignacio José Dasso

## Muy breve descripción del trabajo práctico:
Desarrollo de plataforma para la integración y visualización de datos originados por estaciones de medición vinculadas a la red IoT GEO desplegada por Arsat.
Link: https://docs.google.com/document/d/1MmpQ4RmHmQ25UQEeI_A3iR1Rp0mPJwzN5ye3oOfIFBE/edit?usp=sharing

## Resolución
 * Objetivo del ataque: interrumpir el tráfico de datos de los clientes produciendo que la plataforma no pueda proveer el servicio, retener los datos intervenidos en otra base de datos que permita una potencial devolución futura de los datos.

* Reconnaissance
  - Sé que el servicio consta de una plataforma de visualización de datos (portal).
  - La plataforma tiene que tener acceso para el personal, así que busco nombre de personas (preferentemente vinculadas al proyecto) y estructura típica de los correos para obtener nombre de usuario de la plataforma.
  - Obtengo la URL del portal ofrecido por Arsat.
  - Evalúo qué direcciones IP intervienen al cargar el portal.
  
* Weaponization
  - Decido armar una base de datos gemela a dónde se reeviarán los datos, alterar las configuraciones de origen/destino de la información y aportar información dummy que no alerte de la intervención.
  
* Delivery
  - Phishing: habiendo contactado a la compañía, identifico a un responsable del proyecto y envío un correo solicitando una nueva alta de servicio.
  
* Exploit
  - En el correo incluyo un script que identifica la conexión con el sistema de la plataforma e ingresa haciendo uso de la conexión del infectado.
  
* Installation  
  - Completada la conexión del infectado con la plataforma, se carga el malware.

* Command & Control
  - Confirmo cuáles las conexiones de entrada/salida de datos.
  - Completo configuraciones de reenvío de datos útiles y de provisión de datos dummy.
  
* Actions on Objectives
  - Inicio en simultáneo la inserción de datos dummy y el reenvío de datos a la base de datos gemela.
