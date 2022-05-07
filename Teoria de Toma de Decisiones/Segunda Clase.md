## Teoría de Toma de Decisiones - 06/05/2022
Prof Jose Luis Quintero

![[Recording 20220506115237.webm]]


### 6 - Ambientes en la toma de deciones
 - Bajo Certeza 
 - Bajo Incertidumbre
 - Bajo Riesgo
 
 
 filas alternativas
 columnas estado
 A1
 A2
 A3
 A4
 A5
 
|     | E1       | E2       | E3       | E4       |
| --- | -------- | -------- | -------- | -------- |
| A1  | $V_{11}$ | $V_{12}$ | $V_{13}$ | $V_{14}$ |
| A3  | $\vdots$ | $\vdots$ | $\vdots$ | $\vdots$ |
| A4  | $\vdots$ | $\vdots$ | $\vdots$ | $\vdots$ |
| A5  | $V_{51}$ | $\dots$  | $\dots$  | $V_{55}$ |

#### <ins>Cuadro de cualidades</ins> (atributos/criterios)
| <ins>Cualidades</ins> | Sinforosa | Socorrito |       |       |
| --------------------- | --------- | --------- | ----- | ----- |
| Conversacion          | $-2$      | $4$       | 0     | 1     |
| Personalidad          | $4$       | $3$       | 1     | 0     |
| Inteligencia          | $-4$      | $3$       | 0     | 1     |
| Fisico                | $5$       | $-1$      | 1     | 0     |
| Prestigio de trabajo  | $2$       | $2$       | 0     | 0     |
| Idiomas               | $3$       | $1$       | 1     | 0     |
| Cursos                | $2$       | $1$       | 1     | 0     |
|                       | **$13$**  | **$10$**  | **4** | **2** | 

- Estrategia de impresión global **Sinforosa:** 10 ==**Socorrito:**  13==
- Estrategia de comparación de variable ==**Sinforosa:** 4== **Socorrito:** 2
 ````ad-note

Criterios para poder decidir. Se debe tener una escala para medir todos los atributos.

Unos pueden ser cualitativos o cuantitativos.
````


### Estrategia d eimpresión global
cuando se suma se le da el mismo nivel de importancia

### Comparación de variables
````ad-note
Este metodo no toma en cuenta la diferencia entre las cualidades
````

### Estrategia de adición de pesos
````ad-note
Se debe generar la importancia (el peso)
````

| Atributo           | Peso |
| ------------------ | ---- |
| Inteligencia       | 7    |
| Personalidad       | 4    |
| Atractivo Físico   | 3    |
| **CUALQUIER OTRO** | 1    | 

| <ins>Cualidades</ins> | Sinforosa       | Socorrito       |
| --------------------- | --------------- | --------------- |
| Conversacion          | $(-2)$          | $4$             | 
| Personalidad          | $4 \times 4$    | $3 \times 4$    |
| Inteligencia          | $(-4) \times 7$ | $3 \times 7$    |
| Fisico                | $5 \times 3$    | $(-1) \times 3$ |
| Prestigio de trabajo  | $2$             | $2$             |
| Idiomas               | $3$             | $1$             |
| Cursos                | $2$             | $1$             |
| **TOTAL:**            | **8**           | **38**          |

Estrategia de adición de pesos **Sinforosa:** 8 ==**Socorrito:** 38==

### Nuevo problema (EJEMPLO 4)
Martin es buen estudiante y tiene 3 opciones de universidades que le ofrecen una beca (100%). Martin tiene que decidir entre algunas de ellas.

Martin se va a basar en dos criterios

Ubicación y Reputación

**TOMA DE DECISIONES MULTICRITERIO**

| Atributo   | Peso |
| ---------- | ---- |
| Reputación | 83%  |
| Ubicación  | 17%  | 


| Criterio  | Universidad A | Universidad B | Universidad C |
| --------- | ------------- | ------------- | ------------- |
| Reputción | 12.9%         | 27.7%         | 59.4%         |
| Ubicación | 54.5%         | 27.3%         | 18.2%         | 

| Criterio  | Universidad A       | Universidad B        | Universidad C       |
| --------- | ------------------- | -------------------- | ------------------- |
| Reputción | $0.129 \times 0.83$ | $0.277\times 0.83$   | $0.594\times 0.83$  |
| Ubicación | $0.545 \times 0.17$ | $0.273  \times 0.17$ | $0.182 \times 0.17$ |
| **Total** | $0.4743$            | $0.2737$             | $0.2520$            |

Gana la universidad A

---

| Atributo   | Peso  |
| ---------- | ----- |
| Reputación | $P$   |
| Ubicación  | $1-P$ |

$$0 \le P \le 1$$

$$A=0.129 \times P + 0.545 \times (1-P)$$
$$B=0.277 \times P + 0.273 \times (1-P)$$
$$C=0.594 \times P + 0.182 \times (1-P)$$

Graficas (rectas)
$$A: y=0.129 \times x + 0.545 \times (1-x)$$
$$B: y=0.277 \times x + 0.273 \times (1-x)$$
$$C: y=0.594 \times x + 0.182 \times (1-x)$$

![[Pasted image 20220506112004.png]]

````ad-note
Indiferencia = emplate

La ubicación se puede medir en tiempo o en kilometros
```` 

```plantuml

class A 

```

### Nuevo problema de trabajadores

|     | T1  | T2  | T3  |
| --- | --- | --- | --- |
| A1  | 130 | 105 | 117 |
| A2  | 400 | 435 | 410 |
| A3  | 200 | 200 | 200 |
| A4  | 515 | 500 | 518 | 

**Ideal: **

|     | T1      | T2      | T3      | ==Ideal== | 
| --- | ------- | ------- | ------- | --------- |
| A1  | 130     | ==105== | 117     | 105       |
| A2  | ==400== | 435     | 410     | 400       |
| A3  | ==200== | ==200== | ==200== | 200       |
| A4  | 515     | ==500== | 518     | 500       |

$Punto/vector\,ideal: (105,400,200,500)$
$T1: (130,400,200,515)$

$Distancia = \sqrt{(105-130)^2+(400-400)^2+(200-200)^2+(500-515)^{2}}$

$Distancia = 29.15$

````ad-note
Gana quien tenga menor distancia
````

**Anti-ideal:**

|     | T1      | T2  | T3  | AntiIdeal |
| --- | ------- | --- | --- | --------- |
| A1  | ==130== | 105 | 117 | 130       |
| A   | 515     | 500 | 518 | 518       |

### Proyecto

1. Poner referencias de la ==1==
2. Identificar los elementos de la toma de deciosiones (decisor, alternativa... )
3. Tema de la secretarias con un amigo que tiene 3 instituciones, decidir institución.
4. Costo, modelo (atributos), asumiedo que tienen igual importancia determinar el proceso de jerarquía.

