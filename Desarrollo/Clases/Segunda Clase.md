## Desarrollo del software 4/28/2022
Prof Carlos Alonzo

---

1.  <ins>Ideal</ins> **Cualidades del software**
	1.  Escalabilidad
	2.  <ins>Reusabilidad</ins>
	3.  <ins>Altamente desacoplado</ins> Bajo acomplamiento
	4.  <ins>Extensible</ins>
	5. <ins> Mantenible</ins>
	6.  <ins>Alta cohesión</ins> (SRP y ISP)
	7.   Portable
	8.  <ins>Testability</ins>
	9.  Trabajo en paralelo (SRP) ⭐
	10. <ins>Seguridad</ins> ⭐ - Security by Desing (DDD)
	11. Facilidad de planificar las tareas
2. Diseño  SOLID
3. Teoría de Objetos
4. abstracción / indircción

Se hacen mal y se documenta en el paper que esta malo y como se puede arreglar (un analisis)


Andromeda

### Repaso SOLID

Acomplamiento abstracto
Acomplamiento estructural

#### SRP: Nos invita a pensar en la responsabilidad única
- Alta cohesión
- Responsabilidad única
- Una <ins>clase</ins> tiene una sola razón para <ins>cambiar</ins>
	- Los cambios son constantes y existen dos tipos de cambios (==puntos de variación== y ==puntos de evolución==)
	- **Punto de evolución:** son los que van a cambiar en lo largo del tiempo (⚠ hay que tener cuidado). Lo que especula el equipo técnico que puede cambiar.
	-  **Puntos de variación:** ya estan en los requerimientos, ya está documentado. Esto esta premeditado. 
Aplica para cualquier abstracción clase/agregado/modulo, se aplica a nivel macro y micro. 

Lógica de negocio = DOminio de problema
- Dominio del problema
- Registro - <del>Clase paciente</del> Casos de usos
- Agendar cita - <del>Clase paciente</del> Casos de usos
- Historia médica - <del>Clase paciente</del> Casos de usos

==Una clase por cada CASO DE USO==

````ad-note
title: Investigar

Página del autor donde dice que  "esto te va a ocacionar una..." 
```` 

SI el caso de uso tiene muchos IF, no estamos utilizando un patrón de diseño como es el decorador.

EPICAS, HISTORIAS DE USUARIO.

notificaciones = aspectos
Programación orientada a aspectos
la capa logica vive en la memoria, son objetos

---

Detalles de implementación
-	web
-	Flutter
-	Net
-	BD
- UI
- Frameworks

#### OCP: 
- Abierto para <ins>extesión</ins> : Agregarle funcionalidades
- Cerrado para la <ins>modificación</ins>: Modificar el código que existe
- ==Refactorizar ⭐==

```plantuml
	class Estudiante{
	}

	class Materia{
		-nota
		-
	}
	Estudiante *-- Materia
	
```
---
Algoritmo para calcular el porcentage de credibilidad (indice de credibildiad)

❌ No cumple OCP
```plantuml
	class Doctor{
		- IndiceDeCredibilidad
		- calcularCredibilidad()
	}

	class B as " "{
		
	}
	Doctor *-- B
	
```
 
 ✔ Cumple: 
 
 ```plantuml
	class Doctor{
		- IndiceDeCredibilidad
		- calcularCredibilidad()
	}
	

	class B as "Algoritmo"{
		
		- calcular()
	}
	Doctor *-- B
	
```

 ````ad-note
 ```js
obj.calcular();
 ```
 En clase doctor
 ```` 
---
acoplamiento abstracto (✔positivo)
 ```plantuml
	class Doctor{
		- IndiceDeCredibilidad
		- calcularCredibilidad()
	}
	

	interface B as "Algoritmo"{
		
		- calcular()
	}
	
	class C as "Panama"{
	}
	
	class D as "Otro Pais"{
	
	}
	
	
	Doctor *-- B
	
	B <|-- C
	B <|-- D
	
```

El riesgo es minimo
````ad-note
La clase `Algoritmo` es un inderección

*"...con DDD esto se va a transformar en un servicio de dominio"*
````
Patrón visitor: viola SRP.

#### DIP
- Depender de <ins>abstracciones</ins> y no de <ins>clases concretas</ins>

```plantuml
	class Paciente{
		
	}
	interface PacienteRepositorio{
		+crear()
		+borrar()
		+buscar(String id): Paciente
		+buscar(String nombre, int limit): Paciente
		+buscar(String criterio, int ofset, int limit): Paciente[]
	}
	class a as "MongoDB"{}
	class b as "MySQL"{}
	
	Paciente --> PacienteRepositorio
	PacienteRepositorio <|.. a
	PacienteRepositorio <|.. b
	
	
```



````ad-note

*La interface es un contrato*
Repositorio = almacenar/persistencia

**MongoDB** y **MySQl** son detalles de implementación.

Este diseño tiene de acoplamiento estructural o por primitivas o por que se dejan colar detalles de implementación

se ha dejado colar atravez del tipo de datos de los parametros, los detalles de implementación

Esto se evita con los value objects (DDD).

`String id` = PacienteId
`String nombre` = PacienteNombre

El parameto `int limit` es un anti-patrón

````