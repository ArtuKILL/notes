````ad-note

Hacer una clase mapper que itere cualquier estructura
```` 

````ad-hint
Que todas las esctructuras sean iterables

Iterable: te regresa un iterador.
```` 

coposión de un atron con otro patron

```ad-caution
title: Patron iterator con composite
Cambiar esto
```

```plantuml
interface Component {}

interface Iterable {}

interface Iterator {}

class Composite{}

class Leaf{}

class LeafIterator{}

class CompositeIterator{}

Iterable <|-- Component
Component <|-- Leaf 
Component <|-- Composite 
Component --o Composite
LeafIterator --> Leaf
CompositeIterator --> Composite

CompositeIterator --|> Iterator
LeafIterator --|> Iterator
```

**Inyección de dependecias**
1 - Problema que tenemos y a donde queremos llegar.

**Software:**
- Mantnible
- Extensible
- <ins>Trabajo en paralelo</ins>

**Trabajo en parelelo**
- Buena definición de <ins>Casos de Usos</ins>
- Organización del código (Repo GIt).
- CodeModelGAP
- Arquitectura Software aparece desde la crisis de software.
	- Layers (No tan buena) ❌
		- MVC Pattern/ Antipattrón
	- Inyección de Dependecia
		- por constructor
1 clase por un caso de uso

```plantuml
class A
class B
class C
class D

B <-- A
C <-- A
D <-- A
```

**Tipos de dependencia** 
 - Estables
 - Volatiles

todo lo que no esta heco es una dependencia volatil

dependencia estable: SOn aquellas que ya existen para nosotros, tienen un comportamiento determinista y no necesitaran ser reemplazadas.

String se encapsula en value obcjet

abusar de patrones primitivos ANTI-PATRON

dependencias volatiles: son aquella que estan bajo desarrollo, o no estan disponibles en todas las máquinas de los desarrollos, o contiene un comportamiento no determinista es decir aleatorio, o finalmente pudieran ser reemplazadas.

```ad-hint
las bases de datos son volatiles
```

con inección de dependencia se busca controlar las dependencias volatiles (controla los side effects)
