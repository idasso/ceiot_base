## Ejercicio CiberKillChain - Ataque

#### Alumno: Ignacio José Dasso

## Muy breve descripción del trabajo práctico:
Desarrollo de plataforma para la integración y visualización de datos originados por estaciones de medición vinculadas a la red IoT GEO desplegada por Arsat. [Link](https://docs.google.com/document/d/1MmpQ4RmHmQ25UQEeI_A3iR1Rp0mPJwzN5ye3oOfIFBE/edit?usp=sharing)

## Resolución

### Objetivo del ataque:
* Interrumpir el tráfico de datos de los clientes produciendo que la plataforma no pueda proveer el servicio, retener los datos traficados en una base de datos gemela que permita solicitar un pago a cambio de devolver la información secuestrada.

### Reconnaissance
* Sé que el servicio consta de una plataforma de visualización de datos (portal).
* La plataforma tiene que tener acceso para el personal, así que busco nombre de personas (preferentemente vinculadas al proyecto) y estructura típica de los correos para obtener nombre de usuario de la plataforma.
  -  T1593.001. Investigación de nombre de empleados de Arsat en LinkedIn.
  -  T1589.002. Enumerar direcciones de mail a través de Office 365 [Link](https://github.com/gremwell/o365enum)
* Evalúo qué direcciones IP intervienen al cargar el portal y obtengo la URL del portal ofrecido por Arsat.
  - T1595.001. Escaneo de bloques IP usando consultas y respuestas ICMP. Utilizo las IP que proveen respuesta para identificar diferentes web asociadas a Arsat.
* Identifico dónde está la base de datos y cómo se estructura
  - _Técnica a definir._

### Weaponization
* Decido armar una base de datos gemela a dónde se reeviarán los datos, alterar las configuraciones de origen/destino de la información y aportar información dummy que no alerte de la intervención.
  - En función del reconocimiento, armo la base de datos.
  - Armo también la base de datos que utilizaré para inyectar datos dummy mientras robo los datos útiles. 
* Decido implementar una metodología de Phishing para hacer el delivery
  - Habiendo detectado la identidad de algún referente de proyecto, diseño un mensaje impostando al referente que envíe un "manual actualizado" de la plataforma en PDF a usuarios de la plataforma.
  - Diseño el PDF tal que solicite credenciales del sistema para acceder al contenido.
  
### Delivery
* Phishing: envío el correo diseñado a los usuarios de la plataforma.
  - T1566.001
  
### Exploit
* En el correo incluyo un documento en PDF solicita contraseñas de la plataforma para acceder al contenido.
* Habiendo adquirido los accesos, ingreso a la plataforma y evalúo la forma más adecuada de redirigir la información evitando ser detectado.
* Diseño un script que pueda correr como usuario tal que en simultáneo redireccione los datos al servidor gemelo y comience a inyectar datos desde una base de datos dummy.
* [Delivery] Envío el script a la plataforma
* [Reconnaissance] T1040 - Network sniffing: Inspecciono los datos que se trafican para diseñar los datos dummy que tendrán que estar en la base de datos.
* Defino una regla tal que los datos dummy sean los datos útiles afectados por una función.
  
### Installation  
* Implemento el script en la plataforma tal que esté listo para activar la modificación en la provisión y reenvío de datos en el momento deseado
* Ejecuto una prueba con una operación de tráfico de baja visibilidad o impacto en la plataforma.
* Selecciono los objetivos a atacar por el servicio.

### Command & Control
* Inicio el ataque. Se corre el script reconfigurando las conexiones de entrada/salida de datos.
* Observo que el desempeño de la plataforma no varíe apreciablemente.
  
### Actions on Objectives
* Corroboro que los datos dummy se estén inyectando y que la base de datos gemela esté adquiriendo los datos útiles.
