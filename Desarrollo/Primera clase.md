## Desarrollo del software 4/26/2022
Prof Carlos Alonzo

---
Notas de la primera clase de desarrollo del software, si hay algún error pueden corregirlo 👍.
Más que todo hay información del documento de apoyo de la clase y algúnos diagramas y notas que dio en clase.

Este documento esta hecho para leerse con [obsidian](https://obsidian.md)

---
### Plan de clases
- Estructurado
- Flexible
- Evaluación continua
---
### Evaluaciones
- Individual
- Subgrupos (3 - 4 personas)
- Grupo (10 - 11 estudiantes)
	- El trabajo debe estar avalado a nivel de Repositorio y ==Planificación==

---
### Ciclo de Desarrollo con DDD
 Diseño orientado al dominio, yo diseño mi solución basado en el dominio.
 ![[Pasted image 20220426192410.png]]
 ![[Pasted image 20220426192532.png]]
---
### Diseño  Táctico en DDD
- Diagrama de clases
 ![[Pasted image 20220426192518.png]]

---
### Juego de fichas 🎮
![[Pasted image 20220426192904.png]]

#### Clases
````ad-example
title: Forma \<T> 🔵🔺
collapse: open

```plantuml
class Forma <<T>>{
	+ props...
}
```
````

````ad-example
title: Casilla 🔲
collapse: open

```plantuml
class Casilla{
	+props...
}
```

````

````ad-example
title: Pieza 🧩
collapse: open

```plantuml
class Pieza{
	+props...
}
```` 
---
### Citas que hay que entender (Filosofía) 📚
####  1era Cita
````ad-quote
title: Cita
*“The ==Visitor pattern== is one of the ==behavioral design patterns==. It allows you to define a new operation without changing the ==classes of the entities== on which it operates. The ==pattern== is usually applied in a situation where there are multiple operations that need to be applied to various different elements. It provides a ==flexible== and ==clean== way to add on more of these operations while ==keeping the elements <ins>stable</ins>==. As can be seen from the description, this pattern is very closely linked to the ==Open-Closed Principle==.”*
```` 

##### Glosario
Palabras con su definición en el contexto
- Visitor pattern
- Behavioral desing patterns
- Classes of the entities
- Pattern
- Flexible
- Clean
- Keeping the elements stable
- Open-Closed Principle

#### 2da Cita 
````ad-quote
title: Cita
*"“==Feature tests== verify the application behavior as a whole, but on top of that there are two aspects that no other tests verify in my testing strategy. These are: ==Dependency injection== and ==interception==. In feature tests, I initialize the system by using the same ==composition root== that is used in the production. The only exception is that I ==mock out== some very specific parts of the system like e-mail sending. By using the same ==composition root==, I can be sure that all the components are properly configured to the container. Another closely related topic is interceptors. I use ==interceptors== to implement the ==cross-cutting concerns== like ==logging== and ==auditing==. Because ==feature tests== use ==production composition root==, also ==interceptors== are configured and bound in the process. This enables asserting ==cross-cutting concerns== in the feature tests when appropriate.”"*
```` 

##### Glosario
Palabras con su definición en el contexto
- Feature test
- Dependecy injection
- interception
- composition root
- mock out
- cross-cuitting concerns
- logging
- auditing
- production composition root

#### 3er Cita

---

### Preguntas ¿?
```` ad-question
title: ¿Qué es un nivel de inderección?

Respuesta: Un objeto o capa intermedia que desacopla (¿) una parte del sistema (?)
````
```` ad-question
title: ¿Qué es una abstracción?
Respuesta: 
```` 

---
### Principios SOLID
`⭐ = Principios que se van a tratar`

#### S - SRP (Single Responsability ) ⭐
#### O - OCP (Abierto - Cerrado) ⭐
#### L - LSP (Pricipio de sustitución de Liskov)
#### I - ISP (Principio de segragación de Interfaces) ⭐
#### D - DIP (Principio de inversión de dependenciaas) ⭐⭐⭐
````ad-example
title: Ejemplo en el patrón repository
collapse: closed

#### Ejemplo 1 ❌
```plantuml
class UserDB{
	- props...
	+ create(args...)
	+ delete(args...)
	+ update(args...)
	+ save(args...)
}

package MySql <<Database>>{
	
}

UserDB --> MySql
```
Los metodos create, delete y update tienen directamente hardcodeado los querys en MySql

#### Ejemplo 2 ✔
```plantuml

class User{
 - props...
}

interface UserRepository{
	+ create(args...)
	+ delete(args...)
	+ update(args...)
	+ save(args...)
}

class UserImplementsMySql{
	+ create(args...)
	+ delete(args...)
	+ update(args...)
	+ save(args...)

}

User --> UserRepository
UserImplementsMySql ..|> UserRepository
```
El repositorio en el contexto de CQRS se puede considerar como middleware
```` 



### IMPORTANTE
---

**Para el quiz**: 
Patrón visitor, patrón de diseño de comportamiento, clases Entidades, flexible y limpio, Principio Open-Closed. ==Primera cita== 
![[#1era Cita]]

***
semana 6 feature test, testing strategy, depedecy injection and interception, composition root, mock out, cross-cuting...

alejarse de arquitectura altamente acopladas y compoentes no reutilisables patron decorator


patron decorador para las vistas de flutter

PARCIAL
==Diferencia entre requerimiento funcional y aspecto==
 
 diseño con aspecto fractal
 
 
 	