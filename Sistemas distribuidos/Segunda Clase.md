# Procesos e hilos
## Proceso
Entidad activa que tiene asociado un conjunto de atributos. 
**Atributos:**
- Código
- Datos
- Stack
- Registros e identificador único


Para ejecutar un programa el sistema operativo crea procesadores virtuales que ejecutan un proceso diferente.

Un proceso es un programa en ejecución

 ## Hilos
 Se parecen a los procesos en el sentido que tienen un id, estados, la diferencia es que tienen un proceso padre, comparten la memoria del proceso padre.
 
 el internet es una limitante en un sistema distribuido.
 
 Preferencia en el monitor antes que el semasfaro.
 
 ## Semáforos
 1. Sean n procesos en el vector P(i)
 2. En cada proceso se eecuta un ==wait(s)== antes de la ejecución de la sección crítica.
 3. El primer proceso que cambie el semáforo lo hará del valor 1 al valor 0, cerrando el paso.
 4. Los demás procesos que encuentren el semáforo cerrado (valor 0) se encontraran en la cola de espera de este semáforo.
 5. Una vez que el primer semáforo termine la sección critica, realizará un ==signal(s)==
 6. Un ==signal(s)== habilitara para su ejecución el siguiente proceso de la cola de espera del semáfoto.
 7. Un ==signal(s)== colocara el valor del semáforo en 1.
 8. El semáforo se inicia con 1 para que el primer proceso ingrese a la sección critica con un ==wait(s)==.
 ````ad-note
 title: Nota
 
 La ejecución de ==Wait== y ==Signal== es atómica
 ```` 
 
 
## Algortmo para dos procesos

```java
bandera[0] = false
bandera[1] = false
turno = O 
p0: bandera[O] = true
	turno = 
	while( bandera[1] && turno == 1 ); 
//no hace nada; espera. // sección crítica 
// fin de la sección crítica bandera[0] = false 

p1: bandera[1] = true 
turno = O
while( bandera[0] && turno = O ); //no hace nada; espera. 
// sección crítica
// fin de la sección crítica
bandera[1] = false 
```

Ejecutar programa de las galletas