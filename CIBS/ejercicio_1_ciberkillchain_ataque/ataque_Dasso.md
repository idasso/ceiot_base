## Ejercicio CiberKillChain - Ataque

Alumno: Ignacio José Dasso

## Muy breve descripción del trabajo práctico:
Desarrollo de plataforma para la integración y visualización de datos originados por estaciones de medición vinculadas a la red IoT GEO desplegada por Arsat. [Link](https://docs.google.com/document/d/1MmpQ4RmHmQ25UQEeI_A3iR1Rp0mPJwzN5ye3oOfIFBE/edit?usp=sharing)

## Resolución

### Objetivo del ataque:
* Interrumpir el tráfico de datos de los clientes produciendo que la plataforma no pueda proveer el servicio, retener los datos traficados en una base de datos gemela que permita solicitar un pago a cambio de devolver la información secuestrada.

### Reconnaissance
* Sé que el servicio consta de una plataforma de visualización de datos (portal).
* La plataforma tiene que tener acceso para el personal, así que busco nombre de personas (preferentemente vinculadas al proyecto) y estructura típica de los correos para obtener nombre de usuario de la plataforma.
  -  [T1593.001](https://attack.mitre.org/techniques/T1593/001/). Investigación de nombre de empleados de Arsat en LinkedIn.
  -  [T1589.002](https://attack.mitre.org/techniques/T1589/002/). Enumerar direcciones de mail a través de Office 365 [Link](https://github.com/gremwell/o365enum)
* Evalúo qué direcciones IP intervienen al cargar el portal y obtengo la URL del portal ofrecido por Arsat.
  - [T1595.001](https://attack.mitre.org/techniques/T1595/001/). Escaneo de bloques IP usando consultas y respuestas ICMP. Utilizo las IP que proveen respuesta para identificar diferentes web asociadas a Arsat.
* Identifico dónde está la base de datos y cómo se estructura
  - _Técnica a definir._

### Weaponization
* Decido armar una base de datos gemela a dónde se reeviarán los datos, alterar las configuraciones de origen/destino de la información y aportar información dummy que no alerte de la intervención.
  - En función del reconocimiento, armo la base de datos.
  - Armo también la base de datos que utilizaré para inyectar datos dummy mientras robo los datos útiles. 
* Decido implementar una metodología de Phishing para hacer el delivery
  - Habiendo detectado la identidad de algún referente de proyecto, diseño un mensaje impostando al referente que envíe un "manual actualizado" de la plataforma en PDF a usuarios de la plataforma.
* [T1587.001](https://attack.mitre.org/techniques/T1587/001/):
  - Diseño un malware #1 que infecte la PC del usuario al abrir el PDF, robe contraseñas de navegadores y habilite un acceso remoto.
  - Diseño un malware #2 que en simultáneo redireccione los datos al servidor gemelo y comience a inyectar datos desde una base de datos dummy. [T1565.003](https://attack.mitre.org/techniques/T1565/003/): Defino una regla tal que los datos dummy sean los datos útiles afectados por una función.
  
### Delivery
* Phishing: envío el correo diseñado a los usuarios de la plataforma.
  - [T1566.001](https://attack.mitre.org/techniques/T1566/001/)
  
### Exploit
* [T1555.003](https://attack.mitre.org/techniques/T1555/003/): Robo las credenciales para acceso al portal.
* [T1219](https://attack.mitre.org/techniques/T1219/): Establezco el acceso remoto.
* [T1078.003](https://attack.mitre.org/techniques/T1078/003/): Elevo el privilegio de la cuenta para obtener capacidad de edición del portal.
* [Delivery] Utilizo el acceso remoto para enviar el malware #2 a la PC infectada.
* [Reconnaissance] [T1040](https://attack.mitre.org/techniques/T1040/) - Network sniffing: Inspecciono los datos que se trafican para diseñar los datos dummy que tendrán que estar en la base de datos.
* Selecciono los objetivos a atacar por el servicio.
  
### Installation  
* Tengo las credenciales.
* Instalo el malware #2

### Command & Control
* Altero las conexiones de entrada/salida de datos.
  
### Actions on Objectives
* [T1567.002](https://attack.mitre.org/techniques/T1567/002/) + [T1565.003](https://attack.mitre.org/techniques/T1565/003/): Corroboro que los datos dummy se estén inyectando y que la base de datos gemela esté adquiriendo los datos útiles.
* Una vez adquirido un volumen de datos equivalente a 6 meses intervención, contacto a la víctima y solicito el pago a cambio de la información.
