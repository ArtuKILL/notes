## Desarrollo del software 5/03/2022
Prof Carlos Alonzo

1 Paper -> Martes Semana 4.

Los paper estan relacionados con el proyecto...

### Recordamos DIP...

```plantuml
class A {
}

interface B{
}

class C{
}

class D

A --> B
B <|.. C
B <|.. D
B --o A


```


**Inyección buena ✔**
```java
class A{
	B b;
	A(B b){
		this.b = b;
	}
}
```

**Inyección mala ❌**
```java
class A{
	B b;
	A(C b){
		this.b = b;
	}
}
```

Interfaces reusables, persistencia.

````ad-
````
==Para la tarea definir excepciones!!!==

excepciones estan relacionadas con condiciones de error. 	

### Patron oobservador 
```plantuml
interface Observable{
	+ add(Observer): void
	+ remove(Observer): void
	+ notifyAll(): void
}
```

![[Pasted image 20220504160643.png]]
Una `Chain` es lo mismo que un `Tile`  porque implementan el mismo contrato `Observable`

```java
Observable e = new Tile();
```

Tile <: Observable

<: (Subtipo)

FreeTile <: Tile <: Observable



````ad-note
title: Relación de subtipo

```plantuml
class Objeto{}
class Persona
class Profe
class Est

Objeto <|-- Persona
Persona <|-- Profe
Persona <|-- Est

```
Profe <: Persona

````

Estado

Estado y Comportamiento

Comportamiento

Cita ESTADOS:
- Creada
- Confirmada
- Cancelada
- Eliminada

```plantuml
[*] --> creada 
creada --> Confirmada
Confirmada --> Cancelada
Cancelada --> Confirmada
Cancelada --> Eliminada
Eliminada --> [*]
```


````ad-warning
estudiar funciones de ordn superior. callback en javascript
```` 

LAs inyecciones de dependencias ayudan a desacoplarse de los detalles de implementación.

### ISP - Principio de Segregación de Interfaces

- Los <ins>clientes</ins> de las <ins>interfaces</ins> no dependen de métodos que no usan
- Las <ins>interfaces</ins> pertenecen a los <ins>clientes</ins>

{S}
{O}
{L}
{I}
{D}



### LSP - Principiode sustitución de <ins>Liskov</ins>

Liskov nos van a pedir programación generica

- Invariante de clase: SIempre es verdadero (condiciones)
- Por cada <ins>método</ins>
	- **Precodiciones:** Lo que requiere el método antes que se invoque.
	- **Postcondiciones:** Lo que yo garantizo que se ejecute.
	- 

A <: B

X <: Observable 

Imagen de PimerParcial

EN TIEMPO DE EJECUCIÓN

```java
A a = new A(new C());
.
.
.
a.setB(new B())
```

Ejemplo EXTENSIBILIDAD
````ad-hint
❌No extensibilidad
```java
Class Casilla{
	Casilla c1, c2, c3, c4;
}
```

✔Extensible
```java
Class Casilla{
	//Casilla c1, c2, c3, c4 ... n vecinos; ❌ extensible
	List<Casilla> vecinos;
}
```


````

````ad-quote
title: Definición de Programación General
...PENDIENTE
```` 
 
 Acotar parametro
 
 ```java
class Vecindad <D, C extends Casilla>{

}
````

Clase generica
```java
class Casilla<D>{}

class Ficha<T>{}
```

````ad-note
title: Notica

La programación generica o polimorfismo parametrico favorece la reusabilidad y extensibilidad.
````

Dependecy Injection CAP - 10... SOLID

Casting = mala pactica

`x = (X)obj;`


````ad-hint

Primera entraga cosa oculta para programación generica.

Ver el diseño y evaluar
````

```java
A<T>

//	 A : Clase generica
//	 T : Tipo parametrizado
//	<T>: Libre acotamiento
```

Cuando se acota el tipo parametrizado se tiene que <ins>comportar como un </ins>...  -> <ins>LSP</ins>

