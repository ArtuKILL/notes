## GRASP - Diseño de objetos con RESPONSABILIDADES
![[Pasted image 20220503100413.png]]
### Objetivos
- Definir los patrones
- Aprender a aplicar cinco de los patrones GRASP

### 16.1. Resposabilidades y métodos

UML defne una **responsabilidad** como "un contrato u obligación de un <ins>clasificador</ins>"
LAs responsabilidades estan ligadas con las obligaciones de un objeto en cuanto a su ==comportamiento==. 
**Tipos de responsabilidades:**
- Conocer
	- Conocer los datos privados encapsulados
	- Conocer los objetos relacionados, 
	- Conocer las cosas que puede derivar o calcular.
- Hacer
	- Hacer algo él mismo, como crear un objeto o hacer un cálculo
	- Iniciar una acción en otros objetos
	- Controlar y coordinar actividades en otros objetos.
	Estas responsabilidades se asignan a las clases durante el diseño.
	
### Patrones GRASP
- Experto en Información
- Creador
- Alta Cohesión
- Bajo Acoplamineto
- Controlador
- ...
	
## Experto en Información (o experto)
	
**Solución:** Asignar una responsabilidad a la clase que tiene la información necesaria para realizar la responsabilidad.

**Problema:** ¿Cuál es un principio general para asignar responsabilidades a los objetos?

````ad-quote 
title: Problema...

*"Un Modelo de Diseño podría definir cientos o miles de clases software, y una aplicación podría requerir que se realicen cientos o miles de responsabilidades. Durante el diseño de objetos, cuando se definen las interacciones entre los objetos, tomamos decisiones sobre la asignación de responsabilidades a las clases software. Si se hace bien, los sistemas tienden a ser más fáciles de entender, mantener y ampliar, y existen más oportunidades para reutilizar componentes en futuras aplicaciones."*
	
*"... es un principio de guía básico que se utiliza continuamente en el diseño de objetos. El Experto no pretende ser una idea oscura o extravagante; expresa la ==“intuición”== común de que los objetos hacen las cosas relacionadas con la información que tienen."*
````
	
**Contradiciones: **
````ad-quote
title: Contradicciones...

*"En algunas ocasiones la solución que sugiere el Experto no es deseable, normalmente debido a problemas de acoplamiento y cohesión (estos principios se discutirán más tarde en este capítulo)."*
````

## Creador
**Solución:** Asignar a `B` la responsabilidad de crear una instancia de clase  `A` si se cumple uno o más de los casos siguientes:
- `B` *agrega* obejetos de `A`
- `B` *contiene* objetos de `A`
- `B` *registra* instancias de `A`
- `B` utiliza más *estrechamente* objetos de `A`
- `B` *tiene los datos de inicialización* que se pasarán a un objeto de `A` cuando sea creado (por tanto, `B` es un <ins>Experto</ins> con respecto a la creación de `A`)

`B` es un *creador* de los objetos `A`

Si se puede aplicar más de una opción, inclínese por una clase `B` que *agregue* o contenga la clase `A`

**Problema:** ¿Quién debería ser el responsable de la creación de una nueva instancia de alguna clase?
````ad-quote
title: Problema...
*"La creación de instancias es una de las actividades más comunes en un sistema orientado a objetos. En consecuencia, es útil contar con un principio general para la asignación de las responsabilidades de creación. Si se asignan bien, el diseño puede soportar un bajo acoplamiento, mayor claridad, encapsulación y reutilización"*
```` 

**Contradicciones:**

````ad-quote
title: Contradicciones

*"A menudo, la creación requiere una complejidad significativa, como utilizar instancias recicladas por motivos de rendimiento, crear condicionalmente una instancia a partir de una familia de clases similares basado en el valor de alguna propiedad externa, etcétera. En estos casos, es aconsejable delegar la creación a una clase auxiliar denominada Factoría <ins>\[GHJV9\]</ins> en lugar de utilizar la clase que sugiere el Creador. Las factorías se estudiarán en el Capítulo 23."*
````

**Patrones/Principios relacionados**
- bajo Acoplamiento
- Factoría
- Todo-Parte
````ad-quote
<ins>\[BMRSS96\]</ins> describe un patrón para definir objetos agregados que favorece la encapsulación de componentes
````

## Olimorfismo

**Solución:** 
Cuando las alternativas o comportamientos relacionados varían según el tipo (clase), asigne la responsabilidad para el comportamiento <ins>utilizando operaciones polimórficas</ins> a los tipos para los que varía el comportamiento <sup>1 </sup>. Corolario: No haga comprobaciones acerca del tipo de un objeto y no utilice la lógica condicional para llevar a cabo alternativas diferentes basadas en el tipo

````ad-quote
title: cita de pie de página
<sup>1</sup> El **polimorfismo** tiene varios significados relacionados. En este contexto, significa “asignar el mismo nombre a servicios en diferentes objetos” <ins>\[Coad95\]</ins> cuando los servicios son parecidos o están relacionados. Los diferentes tipos de objetos normalmente implementan un interfaz común o están relacionados en una jerarquía de implementación con una superclase común, pero esto depende del lenguaje; por ejemplo, los lenguajes con ligadura dinámica como Smalltalk no requieren esto. 