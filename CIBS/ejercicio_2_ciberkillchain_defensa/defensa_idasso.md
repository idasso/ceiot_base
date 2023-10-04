# Ejercicio CiberKillChain - Defensa

## Alumno

Ignacio José Dasso  

## Enunciado

Desarrollar la defensa en función del ataque planteado en orden inverso. No es una respuesta a un incidente, hay que detectar el ataque independientemente de la etapa.

Para cada etapa elegir una sola defensa, la más importante, considerar recursos limitados.

## Resolución

### Actions on Objectives
* [M1030](https://attack.mitre.org/mitigations/M1030/): Network segmentation. Separar los diferentes elementos de la red en espacios aislados permitiendo el intercambio únicamente entre servidores autenticados.

### Command & Control
* [M1022](https://attack.mitre.org/mitigations/M1022/): Restrict File and Directory Permissions.
* Monitorear logs de configuración de fuera de períodos de puesta en operación de nuevos servicios.
  
### Installation  
* [M1033](https://attack.mitre.org/mitigations/M1033/): Limit Software Installation.
* Monitorear uso de recursos y desempeño de servidores.

### Exploit
* [DS0009](https://attack.mitre.org/datasources/DS0009/): Detección de procesos vinculados con softwares de control remoto y matar los procesos en curso que no estén autorizados.
* [M1027](https://attack.mitre.org/mitigations/M1027/): Password policies. Definir criterios de cumplimiento obligatorio para la selección y renovación periódica de contraseñas.

### Delivery
* [M1017](https://attack.mitre.org/mitigations/M1017/): User training. Concientizar en riegos asociados a comunicaciones vía mail externas a la organización, buenas prácticas para el uso de recursos de la compañía y la navegación e interacciones en internet.

### Weaponization

### Reconnaissance
