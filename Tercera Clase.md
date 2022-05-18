## Criterios de toma de deciones bajo incertidumbre


### EJemplo

Matriz de beneficios

|     | E1  | E2  | E3  | E4  |
| --- | --- | --- | --- | --- |
| A1  | 5   | 10  | 18  | 25  |
| A2  | 8   | 7   | 8   | 23  |
| A3  | 21  | 18  | 12  | 21  |
| A4  | 30  | 22  | 19  | 15  |

Eliminar alternativa dominada .

En esta matriz no exoste ninguna materia dominada por otra (<ins>criterio de dominación</ins>).

## Criterio de LaPlace

La incertidumbre por que no se sabe que estado de la naturaleza va a ocurrir.

Cuando tu no sepas la probilidad de los estados se asume que todos tienen la misma probabilidad.

Por cada alternativa se saca el promedio de sus valores

**Calculo de <ins>promedio</ins> para cada alternativa**

cada alternativa

A1: 14.5 
A2: 11.5
A3: 18
==A4: 21.5==

Si es matriz de beneficio te quedas con el ==mayor==

si los datos tienen alta variabilidad no es (¿) recomendado (?) 

mientras mas homogeneos esten los datos 

### Desventajas
- Calcular promedio no siempre es lo más efectivo.

## Criterios del optimismo

### Criterio maximax ó minimin.
Criterio de máximo optimismo.
"Siempre" va a ocurrir el mejor caso.

**Optimismo extremo:**

**Beneficio**

|     | E1     | E2  | E3  | E4  |
| --- | ------ | --- | --- | --- |
| A1  | 5      | 10  | 18  | 25  |
| A2  | 8      | 7   | 8   | 23  |
| A3  | 21     | 18  | 12  | 21  |
| A4  | ==30== | 22  | 19  | 15  |

**Costo**

|     | E1    | E2  | E3  | E4  |
| --- | ----- | --- | --- | --- |
| A1  | ==5== | 10  | 18  | 25  |
| A2  | 8     | 7   | 8   | 23  |
| A3  | 21    | 18  | 12  | 21  |
| A4  | 30    | 22  | 19  | 15  |

### Criterio MAXMIN ó MINMAX (Wald)

|     | E1  | E2  | E3  | E4  |
| --- | --- | --- | --- | --- |
| A1  | 5   | 10  | 18  | 25  |
| A2  | 8   | 7   | 8   | 23  |
| A3  | 21  | 18  | 12  | 21  |
| A4  | 30  | 22  | 19  | 15  |

Se elige el menor por cada fila, y se empiza a elegir lo mejor de lo peor
A1: 5
A2: 7
A3: 12
==A4: 15==

### Criterio de Hurwicz
Maneja el coeficiente de optimismo (alfa)
$$ 0 \le \alpha \le 1$$

**Beneficio**

|     | E1  | E2  | E3  | E4  |
| --- | --- | --- | --- | --- |
| A1  | 5   | 10  | 18  | 25  |
| A2  | 8   | 7   | 8   | 23  |
| A3  | 21  | 18  | 12  | 21  |
| A4  | 30  | 22  | 19  | 15  |

$$A_1: 25\alpha+5(1-\alpha)$$
$$A_2: 23\alpha+12(1-\alpha)$$
$$A_3: 21\alpha+12(1-\alpha)$$
$$A_4:30\alpha+15(1-\alpha)$$

Gráfica
$$A_1: 25x+5(1-x)$$
$$A_2: 23x+12(1-x)$$
$$A_3: 21x+12(1-x)$$
$$A_4:30x+15(1-x)$$

![[Pasted image 20220513104836.png]]

**Costos**
$A_1: 25(\alpha-1)+5\alpha$
$A_2: 23(\alpha-1)+12\alpha$
$A_3: 21(\alpha-1)+12\alpha$
$A_4:30(\alpha-1)+15\alpha$


## Criterio del arrepentimiento o de Savage
Psicologicamente es que se elige una alternativa y se piensa en lo que se pierde de lo mejor de las otras.

**<ins>Paso 1</ins>**
	Por cada columna se elige el mayor valor
	$$V:(30,22,19,25)$$

|     | E1     | E2     | E3     | E4     |
| --- | ------ | ------ | ------ | ------ |
| A1  | 5      | 10     | 18     | ==25== | 
| A2  | 8      | 7      | 8      | 23     |
| A3  | 21     | 18     | 12     | 21     |
| A4  | ==30== | ==22== | ==19== | 15     |
	
**<ins>Paso 2</ins>**

|     | E1  | E2  | E3  | E4  |
| --- | --- | --- | --- | --- |
| A1  | 5   | 10  | 18  | 25  |
| A2  | 8   | 7   | 8   | 23  |
| A3  | 21  | 18  | 12  | 21  |
| A4  | 30  | 22  | 19  | 15  |

Le restas $V$ a cada fila.

resultado: Matriz de arrepentimiento

|        | E1  | E2  | E3  | E4  | mayor arrepentimiento |
| ------ | --- | --- | --- | --- | --------------------- |
| A1     | 25  | 12  | 1   | 0   | 25                    |
| A2     | 22  | 15  | 11  | 2   | 22                    |
| ==A3== | 9   | 4   | 7   | 4   | ==9==                 |
| A4     | 0   | 0   | 0   | 10  | 10                    |
|        |     |     |     |     | Se elige el mayor     |

A3

## Criterio de la distancia al peor valor

<ins>Paso 1:</ins>

Elegir el peor valor a cada columna

|     | E1  | E2  | E3  | E4  |
| --- | --- | --- | --- | --- |
| A1  | 5   | 10  | 18  | 25  |
| A2  | 8   | 7   | 8   | 23  |
| A3  | 21  | 18  | 12  | 21  |
| A4  | 30  | 22  | 19  | 15  |

$V: (5,7,8,15)$

<ins>Paso 2:</ins>
Matriz de distancia

|        | E1  | E2  | E3  | E4  |       |
| ------ | --- | --- | --- | --- | ----- |
| A1     | 0   | 3   | 10  | 10  | 0     |
| A2     | 3   | 0   | 0   | 8   | 0     |
| ==A3== | 10  | 11  | 4   | 6   | ==4== | 
| A4     | 25  | 15  | 11  | 0   | 0     |

Los 0 son malos 😡

## Criterio de la robustez


|     | E1  | E2  | E3  | E4  |
| --- | --- | --- | --- | --- |
| A1  | 5   | 10  | 18  | 25  |
| A2  | 8   | 7   | 8   | 23  |
| A3  | 21  | 18  | 12  | 21  |
| A4  | 30  | 22  | 19  | 15  |

**<ins>Estado 1:</ins>**
Maximo valor y minimo valor del estado

**Estado 1:**
Max: 30 Min: 5
$A_1: \frac{30-5}{30-5} = 1$
$A_2: \frac{30-8}{30-5} = \frac{22}{25} = 0.88$
$A_3: \frac{30-21}{30-5} = \frac{9}{25} = 0.36$
$A_4: \frac{30-30}{30-5} = 0$

**Estado 2**
Max: 22 Min: 7

$A_{1}: \frac{22-10}{22-7} = \frac{4}{5} = 0.8$

$A_{2}: \frac{22-7}{22-7} = 1$

$A_{3}: \frac{22-18}{22-7} = \frac{4}{15} = 0.27$

$A_{4}: \frac{22-22}{22-7} = 0$

**Estado 3**
Max: 19 Min: 8 

$A_{1}: \frac{19-18}{19-8}$
$A_{2}: \frac{19-8}{19-8}$
$A_{3}: \frac{12-}{19-8}$
$A_{4}: \frac{}{19-8}$

estad0 4...

|     | E1      | E2     | E3     | E4     | 
| --- | ------- | ------ | ------ | ------ |
| A1  | 1❌     | 0.8 ❌ | 0.09 ✔ | 0  ✔   |
| A2  | 0.88 ❌ | 1  ❌  | 1   ❌ | 0.2 ✔  |
| A3  | 0.36  ✔ | 0.26 ✔ | 0.63 ✔ | 0.4  ✔ |
| A4  | 0   ✔   | 0   ✔  | 0   ✔  | 1   ❌ |

✔=1 ❌=0
A1: 2
A2: 1
A3: 4
A4: 3

en la pregunta del proyecto se una $\beta = 0.7$

todo coeficiente que sea menor o igual que $\beta$ se acepta, en caso contrario se rechaza
