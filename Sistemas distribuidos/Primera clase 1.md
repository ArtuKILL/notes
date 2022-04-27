# 4/26/2022

Quices los viernes!!!

### ¿Que es un sistema distribuido?
- Distintos componentes que esta  en distintos servidores que confoman un sistema.![[Pasted image 20220426083924.png]]
- Interopelabilidad, es migrar sin problema (es mentira, siempre hay problemas, es decir, sin que el usuario se de cuenta xd). 
- Tiene una capa de ==middleware== 

### Carateristicas
![[Pasted image 20220426084256.png]]
#### Compartición de recursos
- Se comparten los recuros (sistemas de archivos, almacenamiento, tiempo en el procesador (?) )
#### Apertura (openness)
- Capacidad de utilizar protocolos estandares, como se tienen distintos componentes en distintos servidores, se comunican con interfaces estandar. Los sistemas distribuidos tienen otros sistemas (clientes). que se comunican con INTERFACES.
#### Concurrencia
- Cuando varios procesos quieren utilizar el mismo recurso. Ejemplo cuando ambos aplicaciones quieren acceder a la misma base de datos (en este caso se encarga el MANEJADOR DE BASE DE DATOS).
- Aqui se refiere a que el usuario/cliente piensa que es el único en utilizar el recurso.

#### Escalabilidad
- Escalar en usuarios, software (componentes).
#### Tolerancia a fallos
- Hay errores que se pueden ocultar, si se cae la red, se corrompe la base de datos se recurre a una ==replica== para ocultar este fallo. 
- Tolerancia a fallos, se lleba a cabo con redundancia.
#### Transparencia
Ocultar al usuario final, hacerle pensar que tiene disponible todos los recursos cuando no es asi.

### RED
Un sistema no distribuido no necesita una red por que todos los procesos estan en una misma máquina, hay distintos tipos de redes.

#### Asunciones erraas con respecto a a red
Cosas que por error se toman por sentado (Se asusmen, cuando no se debería)
![[Pasted image 20220426090647.png]]

### Desafios
#### Heterogeneidad
- Middleware
- Heterogeniedad y código móvil
Se encarga de la traducción entre los distintos tipos de servidores (?)

#### Seguridad
- Denegación de servicio
- Seguridad del código móvil

Como se habla de componentes que estan distribuidos geográficamente, se debe tomar en cuenta la seguridad que exige el lugar geográfico en que se esta.






#### Extensibilidad/escalabilidad
Debido a que hay redes y sistemas distintos, es un desafio
#### Tratamiento de fallos
#### Concurrencia
#### Transparencia

### Ejemplo de sistemas distribuido
Los DNS manejan los dominios en todo el mundo, es un ejemplo absoluto de Sistema Distribuido.

---
Ejemplo de sistema blibiotecario 
![[Pasted image 20220426091824.png]]