## Cap 7 - SRP (Single Responsibility Principle)
---
### Introducción
No confundir SRP que cada modulo soplo haga una sola cosa.
Si existe un principio en el que *una función debería hacer solo y solamente una cosa* ese principio se usa cuando se refactorizan grandes funciones en pequeñas, ==se usa hasta en los niveles más bajos== pero no es uno de los princips SOLID (no es SRP)

**Definición SRP**
````ad-quote
title: Clean Architeture de Robert Martin


*Un modulo debe ser <ins>responsable</ins> de un, y solo un actor*
````
 
 En donde el ==actor== hace referencia a un grupo de usuarios o interesados que quieren cambiar el sistema de cierta forma.
 
 Un modulo en algunos contextos es un archivo fuente (*source ffile*) en otros contextos pueden ser conjuntos de funciones y estructura de datos.
 
### SIntomas de violación al SRP
 
 #### Sistoma 1: Duplicación accidental
 
 La clase `Employee` forma parte de una applicación de nómina y tiene tres metódos que son `calculatePay()`, `reportHours()` y `save()` 

```plantuml
entity CTO{
}
entity CFO{
}
entity COO{
}
class Employee{
+ calculatePay()
+reportHours()
+ save()
}
CFO ...> Employee
CTO ...> Employee
COO ...> Employee
```
 
 Esta clase viola el SRP ya que esos tres metodos son responsables de tres actures muy diferentes entre ellos.
 
 El metodo `calculatePay()`  es especificado por el departamento de contabilidad que le reporta al CFO.
 
 El metodo `reportHours()`  es especificado y usado por el departamento de recursos humanos que le reporta al COO.
 
 El metodo `save()` es especificado por el administrador de la base de datos (DBAs), quien le reporta al CTO.
 
 Poniendo el código fuente de esos tres metodos en una sola clase `Employee` , los desarrolladores han acoplado los actores entre ellos. Esta acoplación puede causar que las acciones del equipo de contabilidad (CFO) afecten algo de lo que dependa el equipo de recursos humanos (COO).
 
 Por ejemplo, suponiendo que las funciónes `calculatePay()` y `reportHours()` comparten un algoritmo para calcular  las horas no extras. Suponiendo que los desarrolladores, que cuidadosamente no duplicaron el código, pusieron el algoritmo en una función llamada `regularHours()`
 
 ```plantuml
 
annotation calculatePay
annotation reportHours
annotation regularHours

calculatePay --> regularHours
reportHours  --> regularHours
 ```
 
 Ahora suponiendo que el equipo CFO decide que la manera que se calculan las horas no extra debe ser modificada. Y en contraste el equipo COO en recursos humanos no quieren esa modificación en particular ya que ellos usan las horas no extra para un proposito distinto.
 
 Un desarrollador es asignado con la tarea de hacer el cambio, y observa que convenientemente  la función `regularHours()` es llamada por  el metodo `calculatePay()` .  Pero desafortunadamente, ese desarrollador no se da cuenta que la función también es llamada por la función `reportHours()`.
 
 El desarrollador hace el cambio requerido y cuidadosamente lo prueba. El equipo CFO valida que la nueva función funcione como se desea, y el sistema es desplegado (*deploy*).
 
 Y claro, el equipo COO no sabe que esta pasando. El personal de recursos humanos continua usando el reporte generado por la función `reportHours()` pero ahora contiene números erroneos. Evenetualmente el problema es descubierto, y  el COO esta enfurecido debido a que los datos erroneos le han costado un presupuesto de millones de dolares. 
 
 Todos hemos visto cosas asi pasar. Esos problemas ocurren porque ponemos código que dependen diferentes actores  en  una próximidad cercana. El SRP dice que  hay *separar el código en los diferentes actores que dependen de él*
 
 Hay muchos otros sistomas que se pueden encontrar, pero todos involucran muchas personas cambiando el mismo archivo ffuente por distintas razones.
 
 Se evade este problema separando el código de los diferentes actores.
 

 
 
 
 
  
### Soluciones
  
#### Primera solución 
Separar los datos de la funciones.  Donde las tres clases comparten acceso a  `EmployeeData` , que es una simple *data structure* sin metodos cada clase mantiene solo el código necesario para esa función.

```plantuml
class PayCalculator{
	+ calculatePay()
}
class HourReporter{
	+ reportHours()
}
class EmployeeSaver{
	+ saveEmployee()
}

interface EmployeeData

EmployeeData <-- PayCalculator
EmployeeData <-- HourReporter
EmployeeData <-- EmployeeSaver

```

El lado malo es que ahora se tienen tres clases que hay que instanciar y tener seguimiento de ellas. Una solución es usar un patrón fachada *(Facade Pattern)* 

```plantuml
class EmployeeFacade{
	+ calculatePay()
	+ reportHours()
	+ save()
}

class PayCalculator{
	+ calculatePay()
}

class HourReporter{
	+ reportHours()
}

class EmployeeSaver{
	+ saveEmployee()
}

interface EmployeeData


EmployeeData <-- PayCalculator
EmployeeData <-- HourReporter
EmployeeData <-- EmployeeSaver

 PayCalculator <-- EmployeeFacade
 HourReporter <-- EmployeeFacade

EmployeeSaver <-- EmployeeFacade

```

`EmployeeFacade` contiene una porción pequeña de código. Que se encarga de instaciar y delegar  a las clases con las funciones.

Algunos desarrolladores prefieren mantener las reglas de negocio cerca de los datos. Esto se puede lograr manteniendo los metodos mas importantes en la clase `Employee`  y usar esa clase como fachada para funciones menos importantes.
```plantuml
class Employee{
	- employeeData
	+ calculatePay()
	+ reportHours ()
	+ save()
}

class HourReporter{
	+ reportHours()
}

class EmployeeSaver{
	+ saveEmployee()
}

Employee --> HourReporter
Employee --> EmployeeSaver
```



## Cap 8 - OCP (Open-Closed Principle)

````ad-quote
title: Cita
Un artefacto de software debe ser abierto para la extensión y cerrado para la modificación
````

En otras palabras el comportamiento de un artefacto de software debe ser extensible, sin tener que modificarse.
![[Pasted image 20220427170949.png]]

```
<I> = interfaces
<DS> = data structure
```

```plantuml
component "Financial Report Controller" as FRC

component "Financial Report Interactor" as FRI

component "Financial Database" as FD

component "Screen Presenter" as SP

component "Print Presenter" as PP

component "Web View" as WV

component "PDF View" as PDFV

FRI <-- FD
FRC -> FRI
FRC <-- SP
FRC <-- PP
SP <-- WV
PP <-- PDFV
```

## Cap 10 -  ISP (Interface Segregation Principle)

Se deriva del siguiente diagrama
```plantuml
class User1{
}
class User2{
}
class User3{
}
class OPS{
	+ op1()
	+ op2()
	+ op3()
}

User1 --> OPS
User2 --> OPS
User3 --> OPS
```

En el diagrama anterior hay muchos usuarios que usan las operaciones de la clase `OPS` .
Asumamos que el `User1` usa solo `op1()` , que `User2` solo `op2()` y que `User3()` solo  `op3()` .

Si te imaginas que la clase `OPS` esta escrita en un lenguaje como Java. Claramente, en ese caso, el código fuente de `User1` sin darte cuenta depende de `op2()` y `op3()`, idenpendientemente si nos lo llama (usa). Esta dependencia significa que un cambio en el código de `op2()` en `OPS` va a forzar a el `User1` a ser recompilado y re-desplegado, incluso si nada de lo que "preocupa" (la clase) haya cambiado realmente.

Este problema se puede resolver segregando las operaciones en interfaces como se muestra en el siguiente diagrama.

```plantuml
class User1{
}
class User2{
}
class User3{
}
class OPS{
	+ op1()
	+ op2()
	+ op3()
}
interface U1Ops{
	+ op1()
}
interface U2Ops{
	+ op2()
}
interface U3Ops{
	+ op3()
}
User1 --> U1Ops
User2 --> U2Ops
User3 --> U3Ops


U1Ops <|.. OPS
U2Ops <|.. OPS
U3Ops <|.. OPS

/'
U1Ops <|-- OPS
U2Ops <|-- OPS
U3Ops <|-- OPS
'/

```

### ISP y el Lenguaje

Claramente, en la descripción dada previamente depende criticamente del tipo lenguaje
. Lenguajes de tipado estático como Java fuerzan a los programadores a crear declaraciones que el usuario debe importar (`import`) o usar (`use`), si no incluir (`include`). Son esta clase de declaraciones  `included` que en el código fuente que crean las dependencias del código fuente que fuerzan la reecompilación y el re-despliegle.

En lenguajes de tipado dinámico como Ruby y Python, estas declaraciones no existen en el código fuente.  En cambio, son inferenciadas en tiempo de ejecución (*runtime*). Asi no hay dependencias del código fuente que fuerzan la recompilación y el re-despliegle. Esto es la primera razón que los lenguajes de tipado dinámico crean sistemas que son más flexibles y menos acoplados que los de tipado estático.

Este factor puede llevarte a la conclusión que el ISP es un problema de lenguaje, en vez de uno de arquitectura.

## ISP y la Arquitectura

Si tomas un paso atras y miras la motivaciones raiz del ISP, puedes ver preocupación más profunda que asecha. En general, es dañino depender en los modulos que contienen más de lo que necesitas. Esto es obviamente verdadero para las dependecias del código fuente que pueden forzar recompilaciones innecesarias y re-despliegues, pero tambien es verdad en un nivel muy alto de arquitectura.

Considerando, por ejemplo, un arquitecto trabajando en un sistema, S. Quiere incluir un cierto *framework*, F, en el sistema. Ahora supon que los autores de F tienen incluido una base de datos en particular, D. Entonces S depende de F que depende de D.

```plantuml

class "System S" as s
class "System F" as f
class "System D" as d

s->f
f->d
```

Ahora supon que D tiene una caracteristicas (*features*) que D F no usa y, antes de eso, que S no le importan para nada. Cambios en esos features en D pueden forzar un re-despliegue de F y, antes de eso, el re-despliegue S. Peor aun, una falla en alguna de esas features en D puede ocacionar fallos en F y S.

### Conclusión
La lección aqui es que depender de algo que trae una "mochila" (*baggage*) que no necesitas puede causarte problemas que no esperabas.

## Cap 11 -DIP - Dependency Inversion Principle

El principio de inversión de dependencias (DIP en inglés) nos dice que el sistema más flexible son esos en los cualas dependencias del código fuente se hacen referencia a solo abstracciones y no concretaciones (clases concretas)

En los lenguajes de tipado estático, como java, las declaraciones de uso, importación e inclusión deben referirse solo a los módulos fuente que contienen interfaces, clases abstractas o algún otro tipo de declaración abstracta. No se debe depender de nada concentrado.

La misma regla se aplica a los lenguajes de escritura dinámica, como Ruby y Python. Las dependencias del código fuente no deben hacer referencia a módulos concrentados. Sin embargo, en estos lenguajes es un poco más difícil definir qué es un módulo concrentrado. En particular, es cualquier módulo en el que se implementan las funciones que se están llamando.

Claramente, tratar esta idea como una regla no es realista, porque los sistemas de software deben depender de muchas instalaciones concretas. Por ejemplo, la clase String en Java es concreta y sería poco realista tratar de forzarla a ser abstracta. La dependencia del código fuente en el java.lang.string concreto no puede y no debe evitarse.

En comparación, la clase String es muy estable. Los cambios a esa clase son muy raros y están estrictamente controlados. Los programadores y arquitectos no tienen que preocuparse por cambios frecuentes y caprichosos en String.   Por estas razones, tendemos a ignorar los antecedentes estables del sistema operativo y las instalaciones de la plataforma cuando se trata de DIP. Toleramos esas dependencias concretas porque sabemos que podemos confiar en que no cambiarán.

Son los elementos concretos volátiles de nuestro sistema de los que queremos evitar depender. Esos son los módulos que estamos desarrollando activamente y que están experimentando cambios frecuentes.

### Stable Abstractions

Cada cambio en una interfaz abstracta corresponde a un cambio en sus implementaciones concretas. Por el contrario, los cambios en implementaciones concretas no siempre, ni siquiera por lo general, requieren cambios en las interfaces que implementan. Por lo tanto, las interfaces son menos volátiles que las implementaciones.

De hecho, los buenos diseñadores y arquitectos de software trabajan duro para reducir la volatilidad de las interfaces. Intentan encontrar formas de agregar funcionalidad a las implementaciones sin realizar cambios en las interfaces. Esto es **Diseño de Software 101**.

La implicación, entonces, es que las arquitecturas de software estables son aquellas que evitan depender de concreciones volátiles y que favorecen el uso de interfaces abstractas estables. Esta implicación se reduce a un conjunto de **prácticas de codificación muy específicas:**

• No se refiera a clases concretas volátiles. Consulte las interfaces abstractas en su lugar. Esta regla se aplica en todos los idiomas, ya sea de tipo estático o dinámico. También impone severas restricciones a la creación de objetos y, en general, impone el uso de Abstract Factories.

• No derivar de clases concretas volátiles. Este es un corolario de la regla anterior, pero merece una mención especial. En los lenguajes tipificados estáticamente, la herencia es la más sólida y rígida de todas las relaciones del código fuente; en consecuencia, debe usarse con mucho cuidado. En los lenguajes tipificados dinámicamente, la herencia es un problema menor, pero sigue siendo una dependencia, y la precaución es siempre la opción más inteligente.

• No anule funciones concretas. Las funciones concretas a menudo requieren dependencias del código fuente. Cuando anula esas funciones, no elimina esas dependencias; de hecho, las hereda. Para administrar esas dependencias, debe hacer que la función sea abstracta y crear múltiples implementaciones.

• Nunca menciones el nombre de algo concreto y volátil. Esto es realmente solo una reafirmación del principio mismo.

### Factories

Para cumplir con estas reglas, la creación de objetos concretos volátiles requiere un manejo especial. Esta precaución está garantizada porque, prácticamente todos los lenguajes, la creación de un objeto requiere una dependencia del código fuente en la definición concreta de ese objeto.

En la mayoría de los lenguajes orientados a objetos, como Java, usaríamos una fábrica abstracta para administrar esta dependencia no deseada.

La Aplicación utiliza el ConcreteImpl a través de la interfaz del Servicio. Sin embargo, la aplicación debe crear instancias de ConcreteImpl de alguna manera. Para lograr esto sin crear una dependencia de código fuente en ConcreteImpl, la aplicación llama al método makeSvc de la interfaz ServiceFactory. Este método lo implementa la clase ServiceFactoryImpl, que se deriva de ServiceFactory. Esa implementación crea una instancia de ConcreteImpl y lo devuelve como un servicio.

![[Pasted image 20220502182107.png]]
(Uso del patrón Abstract Factory para gestionar la dependencia.)

**La línea curva** es un límite arquitectónico. Separa lo abstracto de lo concreto. Todas las dependencias del código fuente cruzan esa línea curva que apunta en la misma dirección, hacia el lado abstracto.

**La línea curva** divide el sistema en dos componentes: uno abstracto y otro concreto. El componente abstracto contiene todas las reglas comerciales de alto nivel de la aplicación. El componente concreto contiene todos los detalles de implementación que manipulan esas reglas comerciales.

Tenga en cuenta que el flujo de control cruza la línea curva en dirección opuesta a las dependencias del código fuente. Las dependencias del código fuente se invierten contra el flujo de control, razón por la cual nos referimos a este **principio como inversión de dependencia.**

###  Concrete Components

El componente concreto de la imagen anterior, contiene una sola dependencia, por lo que viola el DIP. Esto es típico. Las violaciones de DIP no se pueden eliminar por completo, pero se pueden reunir en una pequeña cantidad de componentes concretos y mantenerlos separados del resto del sistema

La mayoría de los sistemas contendrán al menos uno de esos componentes concretos, a menudo llamado main porque contiene la función main1. En el caso ilustrado en la imagen anterior, la función principal crearía una instancia de ServiceFactoryImpl y colocaría esa instancia en una variable global de tipo ServiceFactory. La aplicación luego accedería a la fábrica a través de esa variable global..

### Conclusion

A medida que avanzamos en este libro y cubrimos principios arquitectónicos de alto nivel, el DIP aparecerá una y otra vez. Será el principio organizador más visible en nuestros diagramas de arquitectura. **La línea curva** se convertirá en los límites arquitectónicos en capítulos posteriores. La forma en que las dependencias cruzan esa línea curva en una dirección, y hacia entidades más abstractas, se convertirá en una nueva regla que llamaremos Regla de Dependencia.
