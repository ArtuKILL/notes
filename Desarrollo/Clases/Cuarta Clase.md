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

Regla de dependencia

| Miembro            | Tarea                                                                                                                                                                                 | Commit significativo                                                                                  | Commit HASH                                  |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | -------------------------------------------- |
| Arturo Lecuona     | Historia Medica del Paciente                                                                                                                                                          | Refactorización de los medical records                                                                | `<11bc3186d82bb9c90ba8d36fa18e7d9344c0125d>` |
| Arturo Lecuona     | Auditoria de la Historia Medica                                                                                                                                                       | feat(audit record): patron decorator en RecordChanges                                                 | `<b759cd1e62fbc9b2d90e5154c4b1a27c8a842735>` |
| Rabindra Harichand | El Paciente puede disponer de varios mecanismos de pago y modalidades: Tarjeta de Crédito, PayPal, Pago mensual o anual, Benecio por paquete de empresa (Benecio a Empleados), etc. | PaymentMethod y sus implementaciones (No está en el nombre del commit pero también SubscriptionType ) | `<eb60c7eda9ca7aec85ddb1d953f3839265bcba52>` |
| Manuel De Olival   | Modificar la historia médica por paciente                                                                                                                                             | Implementación modificar historial médico según la especialidad                                       | `<8b7f10dc8b19ca59426bd64b295693b9a4fa27db>` |
| Manuel De Olival   | Doctor crea un Registro de Historia Médica del Paciente                                                                                                                               | Doctor segun su especialidad crea un Registro de Historia Médica del Paciente                         | `<5436bb15832f32a40cb48cb082a9a7e5c59b09db>` |
| Jesus Soares       | Clase Appointment y AppointmentManagerImpl                                                                                                                                            | Encapsulamiento de la clase Appointment e Implementacion de los metodos …                             | `<de846f987935ee909ec30a2a3a2c0f14aca7851d>` |
| Jesus Soares       | Modulo Payment: Clase Payment, PaymentManager y su uso en la clase Patient, clase abstracta SubscriptionType y las 3 implementaciones de PaymentMethod                                | Implementacion del Modulo Payment y su uso en la clase Patient                                        | `<56a4d2c4f7a38a890081778012cc02590c7b6655>` |

|     |     |     |     |     |     |     |     | 
| --- | --- | --- | --- | --- | --- | --- | --- |
| --- | --- | --- | --- |     |     |     |     |
| --- | --- | --- |     |     |     |     |     |
| --- | --- |     |     |     |     |     |     |
| --- |     |     |     |     |     |     |     |

| Miembro            | Tarea                                                                                                                                                                                                                                                                             | Commit significativo                               | Commit HASH                                  |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------- | -------------------------------------------- |
| Rabindra Harichand | A los Pacientes les llegan noticaciones cuando el Doctor le hace un  cambio en su Historia Médica, por ejemplo. Las noticaciones pueden ocurrir para otros eventos en el futuro. Las noticaciones pueden llegar  por SMS, Noticaciones Push, Correo, Llamada Automática, etc. | Creación de las Notificaciones y patrón Observable | `<19217aaa0de5290c47449a32ebe17683e2a40b1c>` | 
| Manuel De Olival   | Cita del Paciente                                                                                                                                                                                                                                                                 | Implementacion Appointment                         | `<b3f94071f241cb6164ecc32ed2b2264df306b0a9>` |
