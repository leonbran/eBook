# Modelos de Poisson

<br><br>

## Introducción

En el capítulo anterior estudiamos los modelos de Markov, una clase de modelos estocásticos en los cuales la evolución de un sistema se describe mediante transiciones aleatorias entre estados. En este capítulo estudiaremos otra clase de modelos estocásticos, particularmente apropiada para describir la **ocurrencia aleatoria de eventos a lo largo del tiempo**.

Muchos fenómenos pueden describirse mediante el conteo del número de veces que ocurre determinado evento durante un intervalo de tiempo o en una región del espacio. Algunos ejemplos son:

* el número de clientes que llegan a un establecimiento durante una hora;
* el número de llamadas que recibe una central telefónica;
* el número de fallas de un componente durante un período de operación;
* el número de defectos encontrados en una longitud determinada de material;
* el número de mutaciones observadas en una secuencia genética;
* el número de partículas detectadas por un instrumento durante un intervalo de tiempo.

En situaciones de este tipo, el resultado de una observación no tiene por qué estar completamente determinado por las condiciones iniciales. En lugar de predecir un único número de eventos, podemos describir la **probabilidad de obtener cada posible número de eventos**.

La distribución de Poisson proporciona uno de los modelos más sencillos y útiles para este propósito.

El objetivo de este capítulo es construir este modelo progresivamente. Comenzaremos recordando las variables aleatorias discretas y la distribución binomial, para posteriormente introducir la distribución de Poisson. Luego estudiaremos el proceso de Poisson, la estimación de su parámetro y algunas técnicas básicas de simulación computacional.

La idea central será pasar de una descripción basada en datos y tasas de ocurrencia a un modelo probabilístico:

$$
\boxed{
\text{fenómeno}
\longrightarrow
\text{eventos}
\longrightarrow
\text{tasa}
\longrightarrow
\text{modelo de Poisson}
}
$$

<br><br>

## Variables aleatorias discretas

Una **variable aleatoria** es una función que asigna un número real a cada resultado posible de un experimento aleatorio.

En este capítulo nos interesan principalmente las **variables aleatorias discretas**, es decir, aquellas que pueden tomar un conjunto finito o numerable de valores.

Por ejemplo, si observamos el número de clientes que llegan a una cafetería durante una hora, podemos definir

$$
X=\text{número de clientes que llegan durante una hora}.
$$

Entonces $X$ puede tomar valores

$$
X=0,1,2,3,\ldots
$$

pero no valores como $2.37$ clientes.

De manera similar, si contamos el número de fallas de una máquina durante un día,

$$
X=\text{número de fallas durante un día},
$$

entonces nuevamente $X$ es una variable aleatoria discreta.

### Función de masa de probabilidad

La distribución de una variable aleatoria discreta puede describirse mediante su **función de masa de probabilidad** (PMF, por sus siglas en inglés):

$$
p_X(x)=P(X=x).
$$

Esta función asigna a cada valor posible de $X$ la probabilidad de que la variable tome dicho valor.

Toda función de masa de probabilidad debe satisfacer

$$
p_X(x)\geq 0
$$

para todo $x$, y

$$
\sum_x p_X(x)=1.
$$

Por tanto, la distribución de una variable aleatoria discreta puede interpretarse como una forma de repartir toda la probabilidad entre los diferentes resultados posibles.

### Ejemplo: suma de dos dados

Consideremos el lanzamiento de dos dados equilibrados y definamos

$$
X=\text{suma de los resultados obtenidos}.
$$

Los valores posibles son

$$
X\in\{2,3,\ldots,12\}.
$$

Existen $36$ resultados elementales igualmente probables. Sin embargo, no todas las sumas tienen la misma probabilidad.

Por ejemplo, la suma $2$ solamente puede obtenerse mediante

$$
(1,1),
$$

mientras que la suma $7$ puede obtenerse mediante

$$
(1,6),(2,5),(3,4),(4,3),(5,2),(6,1).
$$

Por tanto,

$$
P(X=2)=\frac{1}{36},
$$

mientras que

$$
P(X=7)=\frac{6}{36}=\frac16.
$$

La función de masa completa es

$$
p_X(x)=
\frac{1}{36}
(1,2,3,4,5,6,5,4,3,2,1),
$$

para $x=2,\ldots,12$, respectivamente.

Podemos visualizar esta distribución utilizando Python.

```python
import numpy as np
import matplotlib.pyplot as plt

valores = np.arange(2, 13)
frecuencias = np.array([1, 2, 3, 4, 5, 6, 5, 4, 3, 2, 1])
probabilidades = frecuencias / 36

plt.bar(valores, probabilidades)
plt.xlabel("Suma de los dados")
plt.ylabel("Probabilidad")
plt.title("Distribución de la suma de dos dados")
plt.show()
```

Este ejemplo es sencillo, pero introduce una idea fundamental: **un modelo probabilístico no necesariamente predice un único resultado; describe las probabilidades asociadas con los diferentes resultados posibles.**

<br><br>

## La distribución binomial

Antes de introducir el modelo de Poisson conviene estudiar brevemente la distribución binomial, pues existe una relación matemática y conceptual muy importante entre ambas.

Supongamos que realizamos $n$ experimentos independientes, cada uno de los cuales tiene dos resultados posibles:

$$
\text{éxito},\qquad \text{fracaso}.
$$

Supongamos además que la probabilidad de éxito es siempre $p$.

Cada experimento recibe el nombre de **ensayo de Bernoulli**.

Si definimos

$$
X=\text{número de éxitos en }n\text{ ensayos},
$$

entonces $X$ sigue una distribución binomial:

$$
X\sim\operatorname{Binomial}(n,p).
$$

Su función de masa de probabilidad es

$$
P(X=k)
=
\binom{n}{k}
p^k(1-p)^{n-k},
$$

para

$$
k=0,1,\ldots,n.
$$

El término

$$
\binom{n}{k}
$$

representa el número de maneras de seleccionar cuáles de los $n$ ensayos corresponden a los $k$ éxitos.

### Ejemplo

Supongamos que la probabilidad de que una pieza producida por una máquina sea defectuosa es

$$
p=0.05.
$$

Si seleccionamos $10$ piezas de manera independiente y definimos

$$
X=\text{número de piezas defectuosas},
$$

entonces

$$
X\sim\operatorname{Binomial}(10,0.05).
$$

La probabilidad de encontrar exactamente tres piezas defectuosas es

$$
P(X=3)
=
\binom{10}{3}(0.05)^3(0.95)^7.
$$

Numéricamente,

$$
P(X=3)\approx 0.0105.
$$

Es decir, la probabilidad es aproximadamente $1.05%$.

Podemos calcularla directamente en Python:

```python
from math import comb

n = 10
p = 0.05
k = 3

probabilidad = comb(n, k) * p**k * (1-p)**(n-k)

print(probabilidad)
```

La distribución binomial resulta apropiada cuando conocemos el número de ensayos $n$ y nos interesa contar cuántos de ellos producen un determinado resultado.

Sin embargo, existen muchas situaciones en las cuales no tiene sentido fijar de antemano el número de ensayos. Por ejemplo:

> ¿Cuántos clientes llegarán durante la próxima hora?

En este caso no conocemos previamente cuántos "ensayos" ocurrirán. Lo que puede resultar razonable conocer es una **tasa promedio de ocurrencia**.

Esta situación conduce naturalmente al modelo de Poisson.

<br><br>

## De la distribución binomial a la distribución de Poisson

Existe una conexión fundamental entre las distribuciones binomial y de Poisson.

Supongamos que

$$
X_n\sim\operatorname{Binomial}(n,p_n)
$$

y que $n$ es grande mientras que $p_n$ es pequeño, de tal manera que

$$
np_n=\lambda
$$

permanece constante.

En este caso, la distribución binomial puede aproximarse mediante una distribución de Poisson:

$$
\operatorname{Binomial}(n,p_n)
\approx
\operatorname{Poisson}(\lambda).
$$

Esta aproximación es especialmente útil cuando tenemos un gran número de oportunidades para que ocurra un evento, pero la probabilidad de ocurrencia en cada oportunidad es pequeña.

Para entender la conexión, escribamos

$$
p_n=\frac{\lambda}{n}.
$$

Entonces,

$$
P(X_n=k)
=
\binom{n}{k}
\left(\frac{\lambda}{n}\right)^k
\left(1-\frac{\lambda}{n}\right)^{n-k}.
$$

Cuando $n$ crece,

$$
\binom{n}{k}
\left(\frac{\lambda}{n}\right)^k
\longrightarrow
\frac{\lambda^k}{k!},
$$

mientras que

$$
\left(1-\frac{\lambda}{n}\right)^n
\longrightarrow
e^{-\lambda}.
$$

Por tanto,

$$
P(X_n=k)
\longrightarrow
e^{-\lambda}\frac{\lambda^k}{k!}.
$$

Esta expresión define la distribución de Poisson.

La relación puede resumirse como

$$
\boxed{
n\text{ grande},\quad p\text{ pequeño},\quad np=\lambda
\quad\Longrightarrow\quad
\operatorname{Binomial}(n,p)
\approx
\operatorname{Poisson}(\lambda)
}
$$

Esta relación es importante porque muestra que el modelo de Poisson no aparece de manera aislada: puede entenderse como un límite natural de modelos binomiales.

<br><br>

## La distribución de Poisson

Una variable aleatoria discreta $X$ tiene distribución de Poisson con parámetro $\lambda>0$ si

$$
X\sim\operatorname{Poisson}(\lambda)
$$

y su función de masa de probabilidad está dada por

$$
\boxed{
P(X=k)
=
e^{-\lambda}
\frac{\lambda^k}{k!}
}
$$

para

$$
k=0,1,2,\ldots
$$

El parámetro $\lambda$ determina la distribución completa.

Una propiedad particularmente importante es

$$
E[X]=\lambda
$$

y

$$
\operatorname{Var}(X)=\lambda.
$$

Es decir,

$$
\boxed{
E[X]=\operatorname{Var}(X)=\lambda
}
$$

Esta propiedad será útil posteriormente tanto para interpretar el modelo como para estimar su parámetro.

### Interpretación de $\lambda$

En una distribución de Poisson, $\lambda$ representa el **número esperado de eventos** en el intervalo o región que estamos estudiando.

Por ejemplo, si

$$
X\sim\operatorname{Poisson}(5),
$$

podemos interpretar $\lambda=5$ como:

> El número promedio de eventos observados en el intervalo considerado es 5.

Esto no significa que siempre ocurran exactamente cinco eventos.

Podemos observar

$$
0,1,2,3,4,5,6,\ldots
$$

eventos.

El valor $5$ representa únicamente el promedio de largo plazo.

### Ejemplo: llamadas telefónicas

Supongamos que una central recibe en promedio

$$
\lambda=4
$$

llamadas por minuto.

Si $X$ representa el número de llamadas recibidas durante un minuto, podemos modelar

$$
X\sim\operatorname{Poisson}(4).
$$

La probabilidad de recibir exactamente seis llamadas es

$$
P(X=6)
=
e^{-4}\frac{4^6}{6!}.
$$

En Python:

```python
import math

lam = 4
k = 6

probabilidad = math.exp(-lam) * lam**k / math.factorial(k)

print(probabilidad)
```

También podemos utilizar NumPy para generar observaciones de una distribución de Poisson:

```python
import numpy as np

lam = 4

muestra = np.random.poisson(lam, size=20)

print(muestra)
```

Cada elemento de `muestra` representa una posible observación del número de llamadas recibidas durante un minuto.

<br><br>

## Esperanza y varianza

Para una variable aleatoria discreta $X$, la esperanza se define mediante

$$
E[X]
=
\sum_x xP(X=x).
$$

La esperanza representa el valor promedio que obtendríamos al repetir muchas veces el experimento bajo las mismas condiciones.

La varianza mide la dispersión alrededor de la esperanza:

$$
\operatorname{Var}(X)
=
E[(X-E[X])^2].
$$

Una expresión equivalente es

$$
\operatorname{Var}(X)
=
E[X^2]-(E[X])^2.
$$

Para una variable de Poisson,

$$
X\sim\operatorname{Poisson}(\lambda),
$$

se obtiene

$$
E[X]=\lambda
$$

y

$$
\operatorname{Var}(X)=\lambda.
$$

Por tanto, la desviación estándar es

$$
\sigma_X=\sqrt{\lambda}.
$$

Esto permite una primera interpretación cuantitativa del modelo.

Por ejemplo, si

$$
X\sim\operatorname{Poisson}(100),
$$

entonces

$$
E[X]=100,
$$

$$
\operatorname{Var}(X)=100
$$

y

$$
\sigma_X=10.
$$

Por tanto, aunque el número esperado de eventos sea $100$, las observaciones individuales pueden presentar variabilidad alrededor de este valor.

### Comparación con la distribución binomial

Para

$$
X\sim\operatorname{Binomial}(n,p),
$$

tenemos

$$
E[X]=np
$$

y

$$
\operatorname{Var}(X)=np(1-p).
$$

Si $p$ es pequeño,

$$
1-p\approx 1,
$$

y entonces

$$
\operatorname{Var}(X)\approx np.
$$

Como $\lambda=np$,

$$
E[X]\approx\lambda,
\qquad
\operatorname{Var}(X)\approx\lambda.
$$

Esto proporciona otra forma de comprender por qué la distribución de Poisson aparece como una aproximación de la binomial en el régimen de eventos raros.

<br><br>

## El proceso de Poisson

Hasta ahora hemos considerado una variable aleatoria $X$ que cuenta eventos dentro de un intervalo previamente especificado.

Ahora queremos introducir explícitamente el tiempo.

Sea

$$
N(t)
$$

el número de eventos que han ocurrido desde el tiempo $0$ hasta el tiempo $t$.

Un **proceso de Poisson** con tasa $\lambda>0$ es un modelo para la ocurrencia aleatoria de eventos que satisface, entre otras, las siguientes propiedades:

1. $N(0)=0$.
2. Los incrementos correspondientes a intervalos de tiempo disjuntos son independientes.
3. La tasa promedio de ocurrencia de eventos es constante e igual a $\lambda$.
4. El número de eventos durante un intervalo de longitud $t$ sigue una distribución de Poisson con parámetro $\lambda t$.

Por tanto,

$$
\boxed{
N(t)\sim\operatorname{Poisson}(\lambda t)
}
$$

y

$$
\boxed{
P(N(t)=k)
=
e^{-\lambda t}
\frac{(\lambda t)^k}{k!}.
}
$$

Esta expresión constituye una de las fórmulas fundamentales del capítulo.

### Interpretación de la tasa $\lambda$

Es importante distinguir entre una **tasa** y un **número esperado de eventos**.

Si una central recibe en promedio

$$
\lambda=5
$$

llamadas por hora, entonces $\lambda$ tiene unidades

$$
\frac{\text{llamadas}}{\text{hora}}.
$$

Durante un intervalo de duración $t$, el número esperado de llamadas es

$$
E[N(t)]=\lambda t.
$$

Por ejemplo, durante dos horas,

$$
E[N(2)]=5(2)=10.
$$

Así,

$$
N(2)\sim\operatorname{Poisson}(10).
$$

El parámetro de la distribución no es simplemente $\lambda$, sino

$$
\lambda t.
$$

Esta distinción es fundamental para construir correctamente el modelo.

### Ejemplo: llegada de clientes

Supongamos que una tienda recibe en promedio

$$
\lambda=6
$$

clientes por hora.

Queremos calcular la probabilidad de que lleguen exactamente $8$ clientes durante las próximas dos horas.

Como

$$
t=2,
$$

tenemos

$$
\lambda t=12.
$$

Por tanto,

$$
N(2)\sim\operatorname{Poisson}(12).
$$

La probabilidad buscada es

$$
P(N(2)=8)
=
e^{-12}\frac{12^8}{8!}.
$$

En Python:

```python
import math

lam = 6       # clientes por hora
t = 2         # horas
k = 8

mu = lam * t

probabilidad = math.exp(-mu) * mu**k / math.factorial(k)

print(probabilidad)
```

Podemos también calcular la probabilidad de que llegue al menos un cliente:

$$
P(N(t)\geq 1)
=
1-P(N(t)=0).
$$

Como

$$
P(N(t)=0)=e^{-\lambda t},
$$

obtenemos

$$
\boxed{
P(N(t)\geq1)=1-e^{-\lambda t}.
}
$$

Para el ejemplo,

$$
P(N(2)\geq1)=1-e^{-12}.
$$

<br><br>

## El tiempo entre eventos

El proceso de Poisson permite estudiar no solamente cuántos eventos ocurren, sino también cuánto tiempo transcurre entre eventos.

Si los eventos ocurren según un proceso de Poisson con tasa $\lambda$, entonces el tiempo $T$ hasta el siguiente evento sigue una distribución exponencial:

$$
T\sim\operatorname{Exponencial}(\lambda).
$$

Su función de distribución acumulada es

$$
P(T\leq t)
=
1-e^{-\lambda t},
\qquad t\geq0.
$$

Por tanto,

$$
P(T>t)=e^{-\lambda t}.
$$

Esta relación tiene una interpretación sencilla:

$$
P(T>t)
$$

es la probabilidad de que **no ocurra ningún evento durante los próximos $t$ unidades de tiempo**.

Esto coincide exactamente con la interpretación del proceso de Poisson:

$$
P(N(t)=0)=e^{-\lambda t}.
$$

Así,

$$
\boxed{
P(T>t)=P(N(t)=0).
}
$$

La distribución de Poisson y la distribución exponencial representan dos aspectos diferentes del mismo fenómeno:

$$
\boxed{
\begin{array}{c}
\text{Poisson}\\
\text{¿Cuántos eventos ocurren?}
\end{array}
}
\qquad
\boxed{
\begin{array}{c}
\text{Exponencial}\\
\text{¿Cuánto esperamos hasta el siguiente evento?}
\end{array}
}
$$

Esta conexión será particularmente útil para la simulación de procesos de Poisson.

<br><br>

## Simulación de variables de Poisson

Una de las ventajas de los modelos probabilísticos es que podemos generar observaciones artificiales a partir del modelo.

Supongamos nuevamente que

$$
X\sim\operatorname{Poisson}(5).
$$

Podemos generar $10,000$ observaciones mediante NumPy:

```python
import numpy as np

lam = 5
n = 10000

datos = np.random.poisson(lam, size=n)

print("Media:", np.mean(datos))
print("Varianza:", np.var(datos))
```

Como

$$
E[X]=\lambda=5
$$

y

$$
\operatorname{Var}(X)=\lambda=5,
$$

esperamos que, para una muestra suficientemente grande,

$$
\overline X\approx5
$$

y

$$
s^2\approx5.
$$

Podemos visualizar la distribución simulada:

```python
import numpy as np
import matplotlib.pyplot as plt
import math

lam = 5
n = 10000

datos = np.random.poisson(lam, size=n)

valores = np.arange(0, datos.max() + 1)

plt.hist(
    datos,
    bins=np.arange(-0.5, datos.max() + 1.5),
    density=True,
    alpha=0.6
)

pmf = [
    math.exp(-lam) * lam**k / math.factorial(k)
    for k in valores
]

plt.plot(valores, pmf, "o")
plt.xlabel("Número de eventos")
plt.ylabel("Probabilidad")
plt.title("Distribución de Poisson: simulación y modelo")
plt.show()
```

La distribución simulada debería aproximarse progresivamente a la distribución teórica cuando aumenta el tamaño de la muestra.

Esta es una manifestación computacional de la **ley de los grandes números**.

<br><br>

## Simulación de un proceso de Poisson

También podemos simular directamente los tiempos de ocurrencia de los eventos.

Supongamos que los eventos ocurren con tasa

$$
\lambda=3
$$

eventos por unidad de tiempo.

Los tiempos entre eventos siguen una distribución exponencial:

$$
T_i\sim\operatorname{Exponencial}(\lambda).
$$

Si generamos sucesivamente estos tiempos,

$$
T_1,T_2,T_3,\ldots,
$$

los tiempos acumulados de ocurrencia son

$$
S_1=T_1,
$$

$$
S_2=T_1+T_2,
$$

$$
S_3=T_1+T_2+T_3,
$$

y, en general,

$$
S_n=\sum_{i=1}^n T_i.
$$

Cada $S_n$ representa el instante en que ocurre el evento $n$.

En Python podemos realizar esta simulación mediante:

```python
import numpy as np
import matplotlib.pyplot as plt

lam = 3
tiempo_maximo = 10

tiempos_entre_eventos = []

tiempo = 0

while tiempo < tiempo_maximo:
    espera = np.random.exponential(1 / lam)
    tiempo += espera
    
    if tiempo < tiempo_maximo:
        tiempos_entre_eventos.append(tiempo)

print(tiempos_entre_eventos)
```

Podemos visualizar los eventos como puntos sobre el eje temporal:

```python
plt.eventplot(tiempos_entre_eventos)
plt.xlabel("Tiempo")
plt.yticks([])
plt.title("Simulación de un proceso de Poisson")
plt.show()
```

Cada punto representa la ocurrencia de un evento.

Una característica importante de esta representación es que los eventos no aparecen separados por intervalos regulares. Algunas veces ocurren muy cerca unos de otros y otras veces existe un intervalo relativamente largo entre ellos.

Esto permite visualizar una diferencia fundamental entre un proceso determinista y uno estocástico.

En un modelo determinista podríamos tener eventos exactamente cada $1/\lambda$ unidades de tiempo. En el proceso de Poisson, $1/\lambda$ representa únicamente el **tiempo medio entre eventos**.

<br><br>

## Estimación del parámetro de Poisson

En un problema real normalmente no conocemos el valor de $\lambda$.

Supongamos que observamos el número de eventos durante $n$ intervalos equivalentes y obtenemos los datos

$$
x_1,x_2,\ldots,x_n.
$$

Queremos utilizar estos datos para estimar la tasa $\lambda$.

Una primera aproximación consiste en observar que

$$
E[X]=\lambda.
$$

Por tanto, parece natural utilizar la media de los datos:

$$
\hat{\lambda}
=
\overline{x}
=
\frac{1}{n}
\sum_{i=1}^n x_i.
$$

Este estimador puede justificarse formalmente mediante el método de **máxima verosimilitud**.

### Máxima verosimilitud

Supongamos que

$$
X_1,\ldots,X_n
$$

son observaciones independientes de una distribución

$$
\operatorname{Poisson}(\lambda).
$$

La función de verosimilitud es

$$
L(\lambda)
=
\prod_{i=1}^n
P(X_i=x_i).
$$

Como

$$
P(X_i=x_i)
=
e^{-\lambda}
\frac{\lambda^{x_i}}{x_i!},
$$

tenemos

$$
L(\lambda)
=
\prod_{i=1}^n
e^{-\lambda}
\frac{\lambda^{x_i}}{x_i!}.
$$

Por tanto,

$$
L(\lambda)
=
e^{-n\lambda}
\frac{\lambda^{\sum_i x_i}}
{\prod_i x_i!}.
$$

Es más conveniente trabajar con el logaritmo de la verosimilitud:

$$
\ell(\lambda)
=
\log L(\lambda).
$$

Entonces,

$$
\ell(\lambda)
=
-n\lambda
+
\left(\sum_{i=1}^n x_i\right)\log(\lambda)
-
\sum_{i=1}^n\log(x_i!).
$$

Derivando respecto a $\lambda$,

$$
\frac{d\ell}{d\lambda}
=
-n
+
\frac{\sum_i x_i}{\lambda}.
$$

Igualando a cero,

$$
-n+
\frac{\sum_i x_i}{\lambda}=0.
$$

De aquí,

$$
n\lambda=\sum_i x_i,
$$

y obtenemos

$$
\boxed{
\hat{\lambda}
=
\frac{1}{n}\sum_{i=1}^n x_i
=
\overline{x}.
}
$$

Por tanto, el estimador de máxima verosimilitud del parámetro de Poisson es simplemente la media muestral.

Este resultado tiene una interpretación muy natural: **la mejor estimación de la tasa promedio de ocurrencia es el promedio observado de eventos por intervalo**.

<br><br>

## Ejemplo de estimación de una tasa

Supongamos que durante diez horas se registró el siguiente número de llamadas recibidas por una central:

$$
4,\quad 7,\quad 5,\quad 3,\quad 6,
\quad 4,\quad 8,\quad 5,\quad 3,\quad 5.
$$

La estimación de la tasa es

$$
\hat{\lambda}
=
\frac{
4+7+5+3+6+4+8+5+3+5
}{10}.
$$

Por tanto,

$$
\hat{\lambda}=5.
$$

El modelo estimado sería

$$
X\sim\operatorname{Poisson}(5).
$$

Podemos realizar el cálculo mediante Python:

```python
import numpy as np

datos = np.array([4, 7, 5, 3, 6, 4, 8, 5, 3, 5])

lambda_estimado = np.mean(datos)

print("Estimación de lambda:", lambda_estimado)
```

Una vez estimado $\lambda$, podemos utilizar el modelo para realizar predicciones probabilísticas.

Por ejemplo, si los datos representan llamadas por hora y queremos conocer la probabilidad de recibir exactamente ocho llamadas durante una hora futura, podemos calcular

$$
P(X=8)
=
e^{-5}\frac{5^8}{8!}.
$$

En Python:

```python
import math

lam = lambda_estimado
k = 8

probabilidad = math.exp(-lam) * lam**k / math.factorial(k)

print("P(X = 8) =", probabilidad)
```

Aquí aparece uno de los aspectos fundamentales del modelamiento estocástico:

$$
\boxed{
\text{datos}
\rightarrow
\text{estimación de parámetros}
\rightarrow
\text{modelo}
\rightarrow
\text{predicción probabilística}
}
$$

No obtenemos una predicción determinista de ocho llamadas. Obtenemos una probabilidad asociada con ese resultado.

<br><br>

## Un ejemplo completo de modelamiento

Consideremos ahora un problema más completo.

Una empresa registra el número de fallas de un determinado componente durante períodos de una hora. Después de observar el sistema durante diez horas obtiene:

```python
fallas = np.array([2, 0, 1, 3, 2, 1, 4, 2, 1, 3])
```

Queremos:

1. estimar la tasa promedio de fallas;
2. construir un modelo de Poisson;
3. calcular la probabilidad de observar exactamente cinco fallas durante una hora;
4. simular 10 000 horas de funcionamiento.

### Paso 1: estimación de la tasa

La estimación es

$$
\hat{\lambda}
=
\frac{1}{10}
\sum_{i=1}^{10}x_i.
$$

En Python:

```python
import numpy as np

fallas = np.array([2, 0, 1, 3, 2, 1, 4, 2, 1, 3])

lambda_estimado = np.mean(fallas)

print(lambda_estimado)
```

### Paso 2: construcción del modelo

Si obtenemos

$$
\hat{\lambda}=1.9,
$$

nuestro modelo es

$$
X\sim\operatorname{Poisson}(1.9).
$$

### Paso 3: probabilidad de cinco fallas

Calculamos

$$
P(X=5)
=
e^{-1.9}
\frac{1.9^5}{5!}.
$$

En Python:

```python
import math

k = 5
lam = lambda_estimado

probabilidad = math.exp(-lam) * lam**k / math.factorial(k)

print(probabilidad)
```

### Paso 4: simulación

Podemos generar 10 000 observaciones:

```python
simulacion = np.random.poisson(
    lambda_estimado,
    size=10000
)

print("Media simulada:", np.mean(simulacion))
print("Varianza simulada:", np.var(simulacion))
```

Finalmente podemos comparar los datos originales con el modelo:

```python
import matplotlib.pyplot as plt

plt.hist(
    simulacion,
    bins=np.arange(
        -0.5,
        simulacion.max() + 1.5
    ),
    density=True
)

plt.xlabel("Número de fallas")
plt.ylabel("Frecuencia relativa")
plt.title("Simulación del número de fallas")
plt.show()
```

Este ejemplo resume buena parte de la metodología utilizada en el libro:

$$
\boxed{
\text{observaciones}
\rightarrow
\text{modelo}
\rightarrow
\text{parámetros}
\rightarrow
\text{probabilidades}
\rightarrow
\text{simulación}
}
$$

<br><br>

## Aplicaciones del modelo de Poisson

El modelo de Poisson puede utilizarse cuando una variable representa el número de ocurrencias de un evento bajo condiciones apropiadas.

Algunos ejemplos son:

### Llegada de clientes

Si una tienda recibe clientes de manera aproximadamente independiente y a una tasa promedio estable, podemos modelar el número de llegadas durante un intervalo mediante

$$
N(t)\sim\operatorname{Poisson}(\lambda t).
$$

### Llamadas telefónicas

El número de llamadas recibidas por una central durante un intervalo puede modelarse mediante un proceso de Poisson cuando la tasa de llamadas es aproximadamente constante y las llegadas pueden considerarse independientes.

### Fallas de componentes

El número de fallas observadas durante un intervalo de operación puede modelarse mediante Poisson en determinadas condiciones.

### Defectos en materiales

Si estamos interesados en el número de defectos que aparecen en una longitud determinada de material, podemos utilizar un modelo de Poisson siempre que resulte razonable suponer una tasa aproximadamente constante de defectos y una ocurrencia independiente.

### Mutaciones

En ciertos modelos simplificados de genética, el número de mutaciones que ocurren en una región determinada puede representarse mediante una distribución de Poisson.

En todos estos casos es importante recordar que **la distribución de Poisson no debe escogerse únicamente porque la variable sea un conteo**. La elección del modelo depende de los supuestos sobre el mecanismo que genera los eventos.

<br><br>

## ¿Cuándo es razonable utilizar un modelo de Poisson?

El modelo de Poisson resulta particularmente apropiado cuando:

* estamos contando eventos;
* los eventos ocurren dentro de un intervalo temporal o espacial;
* existe una tasa promedio de ocurrencia aproximadamente constante;
* la ocurrencia de un evento no afecta directamente la ocurrencia de otro;
* en intervalos muy pequeños es poco probable que ocurran múltiples eventos simultáneamente.

Estas condiciones constituyen una idealización del fenómeno real.

En una aplicación concreta, debemos preguntarnos siempre:

> ¿Son razonables los supuestos del modelo para el fenómeno que estamos estudiando?

Por ejemplo, si la llegada de clientes a una tienda depende fuertemente de la hora del día, una única tasa constante $\lambda$ probablemente no sea suficiente.

En ese caso podríamos necesitar un modelo con una tasa dependiente del tiempo,

$$
\lambda=\lambda(t),
$$

lo cual conduce a modelos de Poisson no homogéneos. Este tipo de extensión queda fuera del alcance de este capítulo.

De manera similar, si los eventos presentan dependencia entre sí, el modelo de Poisson básico puede dejar de ser adecuado.

Por tanto, una parte esencial del modelamiento consiste no solamente en calcular probabilidades, sino en **evaluar las hipótesis que justifican el modelo**.

<br><br>

## Comparación con los modelos de Markov

Los modelos de Markov y los modelos de Poisson son ambos modelos estocásticos, pero responden a preguntas diferentes.

En un modelo de Markov nos interesa principalmente la evolución de un sistema entre diferentes estados. Por ejemplo,

$$
X_0\rightarrow X_1\rightarrow X_2\rightarrow\cdots
$$

donde las probabilidades de transición determinan la evolución aleatoria.

En un modelo de Poisson nos interesa principalmente el número de eventos que ocurren:

$$
N(t)=\text{número de eventos ocurridos hasta el tiempo }t.
$$

Podemos resumir la diferencia de la siguiente manera:

| Modelo                | Objeto principal            | Pregunta                              |
| --------------------- | --------------------------- | ------------------------------------- |
| Markov                | Estado del sistema          | ¿En qué estado estará el sistema?     |
| Poisson               | Número de eventos           | ¿Cuántos eventos ocurrirán?           |
| Poisson + exponencial | Eventos y tiempos de espera | ¿Cuándo ocurrirá el siguiente evento? |

Esta comparación permite apreciar que los modelos estocásticos constituyen una familia amplia de herramientas. No existe un único modelo estocástico apropiado para todos los fenómenos.

Los modelos de Markov son particularmente útiles cuando el concepto de **estado** es central. Los modelos de Poisson son particularmente útiles cuando el fenómeno puede entenderse como una colección de **eventos que ocurren aleatoriamente**.

<br><br>

## Ideas principales

En este capítulo estudiamos una clase de modelos estocásticos orientados al conteo de eventos.

Las ideas fundamentales pueden resumirse de la siguiente manera.

1. Una variable aleatoria discreta puede utilizarse para representar cantidades obtenidas mediante conteo.

2. La distribución binomial describe el número de éxitos en un número fijo de ensayos independientes.

3. La distribución de Poisson aparece naturalmente como aproximación de la binomial cuando el número de ensayos es grande, la probabilidad de éxito es pequeña y $np=\lambda$ permanece constante.

4. Una variable de Poisson satisface

$$
P(X=k)
=
e^{-\lambda}
\frac{\lambda^k}{k!}.
$$

5. Para una variable de Poisson,

$$
E[X]=\lambda,
\qquad
\operatorname{Var}(X)=\lambda.
$$

6. Si los eventos ocurren mediante un proceso de Poisson con tasa $\lambda$, entonces el número de eventos durante un intervalo de longitud $t$ satisface

$$
N(t)\sim\operatorname{Poisson}(\lambda t).
$$

7. El parámetro $\lambda$ representa una **tasa de ocurrencia**, mientras que $\lambda t$ representa el número esperado de eventos durante un intervalo de duración $t$.

8. Los tiempos entre eventos de un proceso de Poisson siguen una distribución exponencial.

9. Si observamos datos provenientes de una distribución de Poisson, el estimador de máxima verosimilitud de $\lambda$ es

$$
\hat{\lambda}=\overline{x}.
$$

10. Los modelos de Poisson pueden simularse computacionalmente y utilizarse para estudiar la variabilidad de los resultados.

El objetivo principal no es solamente aprender una nueva distribución de probabilidad. Lo importante es reconocer una nueva forma de construir modelos matemáticos:

$$
\boxed{
\text{fenómeno}
\rightarrow
\text{datos}
\rightarrow
\text{supuestos}
\rightarrow
\text{modelo probabilístico}
\rightarrow
\text{estimación}
\rightarrow
\text{predicción}
\rightarrow
\text{simulación}
}
$$

De esta manera, el modelo de Poisson complementa los modelos deterministas y los modelos de Markov estudiados anteriormente, ampliando el repertorio de herramientas disponibles para representar fenómenos reales.

<br><br>

## Ejercicios

### Ejercicio 1. Distribución de Poisson

Sea

$$
X\sim\operatorname{Poisson}(4).
$$

Calcule:

a. $P(X=0)$.

b. $P(X=2)$.

c. $P(X=4)$.

d. $P(X\geq1)$.

e. $E[X]$.

f. $\operatorname{Var}(X)$.

### Ejercicio 2. Llegada de clientes

Una cafetería recibe en promedio $8$ clientes por hora.

Suponga que las llegadas pueden modelarse mediante un proceso de Poisson.

a. ¿Cuál es el número esperado de clientes durante tres horas?

b. ¿Cuál es la probabilidad de que lleguen exactamente $20$ clientes durante tres horas?

c. ¿Cuál es la probabilidad de que no llegue ningún cliente durante treinta minutos?

d. ¿Cuál es la probabilidad de que llegue al menos un cliente durante treinta minutos?

### Ejercicio 3. Llamadas telefónicas

Una central recibe en promedio $12$ llamadas por hora.

a. Construya un modelo de Poisson para el número de llamadas recibidas durante una hora.

b. Calcule la probabilidad de recibir exactamente $15$ llamadas.

c. Calcule la probabilidad de recibir más de $15$ llamadas.

d. Calcule la probabilidad de no recibir llamadas durante los próximos diez minutos.

### Ejercicio 4. Estimación de $\lambda$

Durante diez intervalos de una hora se registró el siguiente número de eventos:

$$
3,\quad 5,\quad 2,\quad 4,\quad 6,
\quad 3,\quad 5,\quad 4,\quad 2,\quad 6.
$$

a. Estime $\lambda$ mediante máxima verosimilitud.

b. Construya el modelo de Poisson correspondiente.

c. Calcule la probabilidad de observar exactamente ocho eventos durante una hora.

d. Utilice Python para simular $10,000$ observaciones del modelo estimado.

e. Compare la media y la varianza de la simulación con los valores teóricos.

### Ejercicio 5. Simulación

Utilice Python para generar $10,000$ observaciones de

$$
X\sim\operatorname{Poisson}(\lambda)
$$

para

$$
\lambda=1,\quad 5,\quad 10,\quad 20.
$$

Para cada caso:

a. calcule la media muestral;

b. calcule la varianza muestral;

c. compare estos valores con la media y varianza teóricas;

d. construya las distribuciones empíricas;

e. analice cómo cambia la forma de la distribución cuando aumenta $\lambda$.

### Ejercicio 6. Proceso de Poisson

Suponga que los eventos ocurren con una tasa

$$
\lambda=2
$$

eventos por hora.

Simule durante $24$ horas un proceso de Poisson utilizando tiempos entre eventos generados mediante una distribución exponencial.

a. Determine el número total de eventos simulados.

b. Grafique los tiempos de ocurrencia.

c. Calcule el tiempo promedio entre eventos.

d. Compare el resultado con el valor teórico

$$
E[T]=\frac{1}{\lambda}.
$$

e. Repita la simulación varias veces y estudie la variabilidad del número total de eventos.

### Ejercicio 7. Binomial y Poisson

Considere

$$
X\sim\operatorname{Binomial}(1000,0.002).
$$

a. Calcule la media y la varianza de $X$.

b. Utilice la aproximación de Poisson con

$$
\lambda=np.
$$

c. Calcule mediante ambos modelos la probabilidad

$$
P(X=3).
$$

d. Compare los resultados.

e. Repita el procedimiento para diferentes valores de $n$ y $p$ manteniendo $np$ constante.

### Ejercicio 8. Evaluación de un modelo

Una empresa afirma que el número de fallas de sus dispositivos puede modelarse mediante una distribución de Poisson.

Durante veinte períodos equivalentes se observaron diferentes cantidades de fallas.

Utilice los datos proporcionados por el docente para:

a. estimar $\lambda$;

b. calcular la media y varianza observadas;

c. compararlas con las predicciones del modelo;

d. construir un histograma de los datos;

e. superponer la distribución de Poisson estimada;

f. discutir si el modelo parece razonable;

g. identificar posibles razones por las cuales los datos podrían alejarse del modelo de Poisson.

### Ejercicio 9. Proyecto computacional

Seleccione un fenómeno real que pueda describirse mediante el conteo de eventos.

Algunas posibilidades son:

* llamadas recibidas;
* mensajes recibidos;
* clientes que llegan;
* fallas de un dispositivo;
* accidentes;
* defectos de fabricación;
* eventos deportivos;
* ocurrencia de determinados fenómenos naturales.

Recolecte o utilice un conjunto de datos y realice las siguientes actividades:

1. Defina claramente la variable aleatoria.
2. Especifique la unidad temporal o espacial utilizada.
3. Estime el parámetro $\lambda$.
4. Construya el modelo de Poisson.
5. Calcule algunas probabilidades de interés.
6. Simule observaciones mediante Python.
7. Compare los datos observados con los datos simulados.
8. Discuta las hipótesis necesarias para que el modelo sea razonable.
9. Indique posibles limitaciones del modelo.

El propósito del ejercicio no es solamente obtener un valor para $\lambda$, sino recorrer el proceso completo de construcción y evaluación de un modelo estocástico.
