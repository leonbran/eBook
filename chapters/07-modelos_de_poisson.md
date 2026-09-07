# Modelos de Poisson

<br><br>

## 1. Introducción

En el capítulo anterior estudiamos los modelos de Markov, una clase de modelos estocásticos en los cuales la evolución de un sistema se describe mediante transiciones aleatorias entre diferentes estados. En este capítulo estudiaremos otra clase de modelos estocásticos, particularmente apropiada para describir la **ocurrencia aleatoria de eventos**.

En numerosos fenómenos de interés no estamos interesados principalmente en determinar el estado de un sistema, sino en contar cuántas veces ocurre determinado evento durante un intervalo de tiempo o dentro de una región del espacio.

Por ejemplo:

* el número de clientes que llegan a un establecimiento durante una hora;
* el número de llamadas que recibe una central telefónica;
* el número de fallas de un componente durante un período de operación;
* el número de defectos encontrados en una determinada longitud de material;
* el número de mutaciones observadas en una secuencia genética;
* el número de partículas detectadas por un instrumento durante un intervalo de tiempo.

En situaciones de este tipo, el número de eventos observados no está completamente determinado por las condiciones iniciales del sistema. En consecuencia, en lugar de predecir un único valor, podemos describir las probabilidades asociadas con los diferentes resultados posibles.

La **distribución de Poisson** proporciona uno de los modelos más sencillos para representar este tipo de situaciones.

El propósito de este capítulo no es desarrollar una teoría general de las distribuciones de probabilidad, sino introducir una herramienta de modelamiento que permita describir, analizar, simular y estimar fenómenos caracterizados por la ocurrencia de eventos.

El recorrido que seguiremos será

$$
\boxed{
\text{conteo de eventos}
\longrightarrow
\text{distribución de Poisson}
\longrightarrow
\text{proceso de Poisson}
\longrightarrow
\text{estimación}
\longrightarrow
\text{simulación}
}
$$

La distribución binomial será utilizada como punto de partida para comprender por qué la distribución de Poisson aparece de manera natural en problemas relacionados con eventos poco frecuentes.

<br><br>

## 2. La distribución binomial

Antes de introducir la distribución de Poisson, recordemos brevemente la distribución binomial. Su importancia en este capítulo se debe principalmente a la relación que existe entre ambos modelos.

<br><br>

### 2.1. Ensayos de Bernoulli

Supongamos que realizamos un experimento que puede producir únicamente dos resultados:

$$
\text{éxito},\qquad \text{fracaso}.
$$

Un experimento de este tipo se denomina **ensayo de Bernoulli**.

Supongamos que la probabilidad de éxito es $p$. Entonces

$$
P(\text{éxito})=p
$$

y

$$
P(\text{fracaso})=1-p.
$$

Si realizamos $n$ ensayos independientes bajo las mismas condiciones, podemos definir

$$
X=\text{número de éxitos obtenidos en los }n\text{ ensayos}.
$$

En este caso,

$$
X\sim\operatorname{Binomial}(n,p).
$$

La función de masa de probabilidad es

$$
\boxed{
P(X=k)
=
\binom{n}{k}
p^k(1-p)^{n-k}
}
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

Además,

$$
E[X]=np
$$

y

$$
\operatorname{Var}(X)=np(1-p).
$$

<br><br>

### 2.2. Ejemplo: piezas defectuosas

Supongamos que la probabilidad de que una pieza producida por una máquina sea defectuosa es

$$
p=0.05.
$$

Seleccionamos diez piezas de manera independiente y definimos

$$
X=\text{número de piezas defectuosas}.
$$

Entonces

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

Por tanto, la probabilidad es aproximadamente del $1.05%$.

Podemos calcularla utilizando Python:

```python
from math import comb

n = 10
p = 0.05
k = 3

probabilidad = comb(n, k) * p**k * (1 - p)**(n - k)

print(probabilidad)
```

La distribución binomial resulta apropiada cuando conocemos de antemano el número de ensayos $n$ y queremos contar cuántos de ellos producen determinado resultado.

Sin embargo, existen muchas situaciones en las que no tiene sentido fijar previamente el número de ensayos.

Por ejemplo:

> ¿Cuántos clientes llegarán a una cafetería durante la próxima hora?

En este caso no conocemos de antemano cuántas oportunidades habrá para que ocurra una llegada. En cambio, podemos disponer de información sobre una **tasa promedio de ocurrencia**.

Esta situación conduce naturalmente al modelo de Poisson.

<br><br>

## 3. De la distribución binomial a la distribución de Poisson

La distribución de Poisson puede entenderse como un límite de la distribución binomial en un régimen particular.

Supongamos que

$$
X_n\sim\operatorname{Binomial}(n,p_n),
$$

donde $n$ es grande y $p_n$ es pequeño.

Supongamos además que

$$
np_n=\lambda
$$

permanece constante.

En estas condiciones,

$$
\operatorname{Binomial}(n,p_n)
\approx
\operatorname{Poisson}(\lambda).
$$

Esta aproximación es especialmente útil cuando existe un gran número de oportunidades para que ocurra un evento, pero la probabilidad de ocurrencia en cada oportunidad es pequeña.

<br><br>

### 3.1. Obtención de la aproximación

Tomemos

$$
p_n=\frac{\lambda}{n}.
$$

La probabilidad binomial de obtener exactamente $k$ éxitos es

$$
P(X_n=k)
=
\binom{n}{k}
\left(\frac{\lambda}{n}\right)^k
\left(1-\frac{\lambda}{n}\right)^{n-k}.
$$

Podemos escribir

$$
\binom{n}{k}
\left(\frac{\lambda}{n}\right)^k
=
\frac{n(n-1)\cdots(n-k+1)}{k!}
\frac{\lambda^k}{n^k}.
$$

Para $k$ fijo, cuando $n$ tiende a infinito,

$$
\frac{n(n-1)\cdots(n-k+1)}{n^k}
\longrightarrow 1.
$$

Por tanto,

$$
\binom{n}{k}
\left(\frac{\lambda}{n}\right)^k
\longrightarrow
\frac{\lambda^k}{k!}.
$$

Por otro lado,

$$
\left(1-\frac{\lambda}{n}\right)^n
\longrightarrow e^{-\lambda}.
$$

Además,

$$
\left(1-\frac{\lambda}{n}\right)^{-k}
\longrightarrow1.
$$

En consecuencia,

$$
P(X_n=k)
\longrightarrow
e^{-\lambda}
\frac{\lambda^k}{k!}.
$$

Esta es precisamente la función de masa de probabilidad de una distribución de Poisson.

Así obtenemos

$$
\boxed{
\operatorname{Binomial}(n,p)
\approx
\operatorname{Poisson}(\lambda),
\qquad
\lambda=np,
}
$$

cuando $n$ es grande y $p$ es pequeño.

<br><br>

### 3.2. Interpretación

La aproximación anterior proporciona una interpretación intuitiva del modelo de Poisson.

Supongamos que tenemos muchas oportunidades para que ocurra un evento, pero cada oportunidad tiene una probabilidad muy pequeña de producirlo.

En lugar de especificar explícitamente cada una de esas oportunidades, podemos describir el fenómeno mediante una única cantidad:

$$
\lambda=np,
$$

que representa el número esperado de eventos.

Así, el modelo de Poisson permite pasar de una descripción basada en muchos ensayos individuales a una descripción basada en una **tasa o número esperado de eventos**.

<br><br>

## 4. La distribución de Poisson

Una variable aleatoria $X$ tiene distribución de Poisson con parámetro $\lambda>0$ si

$$
X\sim\operatorname{Poisson}(\lambda)
$$

y

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

El parámetro $\lambda$ determina completamente la distribución.

<br><br>

### 4.1. Interpretación del parámetro $\lambda$

Una característica fundamental de la distribución de Poisson es

$$
E[X]=\lambda.
$$

Por tanto, $\lambda$ representa el **número esperado de eventos en el intervalo o región que estamos estudiando**.

Por ejemplo, si

$$
X\sim\operatorname{Poisson}(5),
$$

entonces

$$
E[X]=5.
$$

Esto no significa que siempre observemos exactamente cinco eventos.

Una observación particular puede producir

$$
0,1,2,3,\ldots
$$

eventos.

El valor $5$ representa el promedio que esperaríamos obtener al repetir el experimento muchas veces bajo las mismas condiciones.

<br><br>

### 4.2. Esperanza y varianza

Para una variable de Poisson,

$$
E[X]=\lambda
$$

y

$$
\operatorname{Var}(X)=\lambda.
$$

Por tanto,

$$
\boxed{
E[X]=\operatorname{Var}(X)=\lambda.
}
$$

La desviación estándar es

$$
\sigma_X=\sqrt{\lambda}.
$$

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

Así, el número esperado de eventos es $100$, mientras que la variabilidad típica alrededor de este valor está asociada con una desviación estándar de $10$.

<br><br>

### 4.3. Ejemplo: llamadas telefónicas

Supongamos que una central telefónica recibe en promedio cuatro llamadas por minuto.

Si $X$ representa el número de llamadas recibidas durante un minuto, podemos plantear

$$
X\sim\operatorname{Poisson}(4).
$$

La probabilidad de recibir exactamente seis llamadas es

$$
P(X=6)
=
e^{-4}\frac{4^6}{6!}.
$$

Podemos calcularla mediante Python:

```python
import math

lam = 4
k = 6

probabilidad = math.exp(-lam) * lam**k / math.factorial(k)

print(probabilidad)
```

También podemos generar observaciones aleatorias del modelo:

```python
import numpy as np

lam = 4

muestra = np.random.poisson(lam, size=20)

print(muestra)
```

Cada elemento de `muestra` representa una posible observación del número de llamadas recibidas durante un minuto.

<br><br>

### 4.4. Visualización de la distribución

Podemos visualizar la distribución de Poisson para diferentes valores de $\lambda$.

```python
import numpy as np
import matplotlib.pyplot as plt
import math

lam = 5

k = np.arange(0, 20)

probabilidades = [
    math.exp(-lam) * lam**x / math.factorial(x)
    for x in k
]

plt.bar(k, probabilidades)

plt.xlabel("Número de eventos")
plt.ylabel("Probabilidad")
plt.title("Distribución de Poisson")
plt.show()
```

El valor de $\lambda$ determina tanto la posición como la dispersión de la distribución.

Cuando $\lambda$ aumenta, el número esperado de eventos aumenta y la distribución se desplaza hacia valores mayores.

<br><br>

## 5. El proceso de Poisson

La distribución de Poisson describe el número de eventos observado dentro de un intervalo previamente especificado.

Ahora queremos incorporar explícitamente el tiempo.

Sea

$$
N(t)
$$

el número de eventos que han ocurrido desde el instante $0$ hasta el instante $t$.

Un **proceso de Poisson** con tasa $\lambda>0$ es un modelo para la ocurrencia de eventos que satisface las siguientes propiedades fundamentales:

1. $N(0)=0$.
2. Los eventos ocurridos en intervalos de tiempo disjuntos son independientes.
3. La tasa promedio de ocurrencia de eventos es constante e igual a $\lambda$.
4. El número de eventos durante un intervalo de longitud $t$ sigue una distribución de Poisson con parámetro $\lambda t$.

En particular,

$$
\boxed{
N(t)\sim\operatorname{Poisson}(\lambda t).
}
$$

Por tanto,

$$
\boxed{
P(N(t)=k)
=
e^{-\lambda t}
\frac{(\lambda t)^k}{k!}.
}
$$

Esta es la expresión fundamental del proceso de Poisson.

<br><br>

### 5.1. Tasa de ocurrencia

Es importante distinguir entre la tasa $\lambda$ y el número esperado de eventos.

Supongamos que una tienda recibe en promedio

$$
\lambda=5
$$

clientes por hora.

Aquí $\lambda$ tiene unidades

$$
\frac{\text{clientes}}{\text{hora}}.
$$

Durante un intervalo de duración $t$, el número esperado de clientes es

$$
E[N(t)]=\lambda t.
$$

Por ejemplo, durante dos horas,

$$
E[N(2)]=5(2)=10.
$$

Por tanto,

$$
N(2)\sim\operatorname{Poisson}(10).
$$

Así, $\lambda$ es una **tasa**, mientras que $\lambda t$ es el **número esperado de eventos durante el intervalo considerado**.

Esta distinción es fundamental al construir un modelo de Poisson.

<br><br>

### 5.2. Ejemplo: llegada de clientes

Supongamos que una cafetería recibe en promedio

$$
\lambda=6
$$

clientes por hora.

Queremos calcular la probabilidad de que lleguen exactamente ocho clientes durante las próximas dos horas.

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

lam = 6
t = 2
k = 8

mu = lam * t

probabilidad = math.exp(-mu) * mu**k / math.factorial(k)

print(probabilidad)
```

<br><br>

### 5.3. Probabilidad de que ocurra al menos un evento

Una pregunta particularmente frecuente es:

> ¿Cuál es la probabilidad de que ocurra al menos un evento durante un intervalo de duración $t$?

Podemos utilizar el complemento:

$$
P(N(t)\geq1)
=
1-P(N(t)=0).
$$

Como

$$
P(N(t)=0)
=
e^{-\lambda t},
$$

obtenemos

$$
\boxed{
P(N(t)\geq1)
=
1-e^{-\lambda t}.
}
$$

Por ejemplo, si una central recibe en promedio

$$
\lambda=4
$$

llamadas por hora, la probabilidad de recibir al menos una llamada durante treinta minutos es

$$
P(N(0.5)\geq1)
=
1-e^{-4(0.5)}
=
1-e^{-2}.
$$

En Python:

```python
import math

lam = 4
t = 0.5

probabilidad = 1 - math.exp(-lam * t)

print(probabilidad)
```

<br><br>

### 5.4. Incrementos independientes

Una propiedad importante del proceso de Poisson es la independencia de los incrementos.

Si $0\leq t_1<t_2<t_3$, entonces el número de eventos ocurrido durante

$$
[t_1,t_2]
$$

es independiente del número de eventos ocurrido durante

$$
[t_2,t_3].
$$

Además,

$$
N(t_2)-N(t_1)
\sim
\operatorname{Poisson}
\left(\lambda(t_2-t_1)\right).
$$

Esta propiedad permite analizar diferentes intervalos de tiempo de manera separada.

Por ejemplo, si una central recibe llamadas a una tasa constante de $10$ llamadas por hora, entonces el número de llamadas durante un intervalo de quince minutos sigue una distribución

$$
\operatorname{Poisson}(2.5),
$$

pues

$$
10(0.25)=2.5.
$$

<br><br>

## 6. El tiempo entre eventos

El proceso de Poisson permite estudiar una segunda pregunta:

> ¿Cuánto tiempo debemos esperar hasta que ocurra el siguiente evento?

Esta pregunta conduce a la distribución exponencial.

<br><br>

### 6.1. Distribución exponencial

Supongamos que los eventos ocurren según un proceso de Poisson con tasa $\lambda$.

Sea $T$ el tiempo de espera hasta el siguiente evento.

Entonces

$$
T\sim\operatorname{Exponencial}(\lambda).
$$

Para determinar su distribución observemos que

$$
P(T>t)
$$

es precisamente la probabilidad de que no ocurra ningún evento durante los primeros $t$ minutos.

Por tanto,

$$
P(T>t)
=
P(N(t)=0).
$$

Como

$$
N(t)\sim\operatorname{Poisson}(\lambda t),
$$

tenemos

$$
P(N(t)=0)
=
e^{-\lambda t}.
$$

Por consiguiente,

$$
\boxed{
P(T>t)=e^{-\lambda t}.
}
$$

Equivalentemente,

$$
\boxed{
P(T\leq t)=1-e^{-\lambda t}.
}
$$

<br><br>

### 6.2. Tiempo medio entre eventos

Para una variable exponencial con parámetro $\lambda$,

$$
E[T]=\frac{1}{\lambda}.
$$

Por ejemplo, si una central recibe

$$
\lambda=4
$$

llamadas por hora, el tiempo medio entre llamadas es

$$
E[T]=\frac14\text{ horas}.
$$

Como

$$
\frac14\text{ horas}=15\text{ minutos},
$$

el tiempo medio entre llamadas es de quince minutos.

Esto no significa que siempre debamos esperar exactamente quince minutos. Nuevamente, se trata de un valor promedio.

<br><br>

### 6.3. Dos perspectivas del mismo proceso

El proceso de Poisson puede analizarse desde dos perspectivas complementarias:

$$
\boxed{
\text{Poisson}
\quad\longrightarrow\quad
\text{¿Cuántos eventos ocurren?}
}
$$

y

$$
\boxed{
\text{Exponencial}
\quad\longrightarrow\quad
\text{¿Cuánto tiempo esperamos?}
}
$$

La primera perspectiva se concentra en el conteo de eventos y la segunda en los tiempos de espera.

Esta relación será útil para simular procesos de Poisson.

<br><br>

## 7. Estimación del parámetro

En una aplicación real normalmente no conocemos el valor de $\lambda$.

Supongamos que observamos el número de eventos durante $n$ intervalos equivalentes y obtenemos los datos

$$
x_1,x_2,\ldots,x_n.
$$

Queremos utilizar estos datos para estimar la tasa $\lambda$.

Una primera observación es que

$$
E[X]=\lambda.
$$

Por tanto, parece natural estimar $\lambda$ mediante la media de los datos:

$$
\hat{\lambda}
=
\overline{x}
=
\frac{1}{n}
\sum_{i=1}^{n}x_i.
$$

Este resultado puede justificarse formalmente mediante máxima verosimilitud.

<br><br>

### 7.1. Máxima verosimilitud

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
\prod_{i=1}^{n}
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
\prod_{i=1}^{n}
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

Es conveniente utilizar el logaritmo de la verosimilitud:

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
\left(\sum_{i=1}^{n}x_i\right)\log\lambda
-
\sum_{i=1}^{n}\log(x_i!).
$$

Derivando respecto a $\lambda$,

$$
\frac{d\ell}{d\lambda}
=
-n
+
\frac{\sum_i x_i}{\lambda}.
$$

Para encontrar el máximo igualamos a cero:

$$
-n+
\frac{\sum_i x_i}{\lambda}=0.
$$

Por tanto,

$$
n\lambda
=
\sum_i x_i,
$$

y obtenemos

$$
\boxed{
\hat{\lambda}
=
\frac{1}{n}
\sum_{i=1}^{n}x_i
=
\overline{x}.
}
$$

Así, el estimador de máxima verosimilitud de $\lambda$ coincide con la media muestral.

<br><br>

### 7.2. Ejemplo de estimación

Supongamos que durante diez horas se registró el siguiente número de llamadas:

$$
4,\quad 7,\quad 5,\quad 3,\quad 6,
\quad 4,\quad 8,\quad 5,\quad 3,\quad 5.
$$

La estimación de $\lambda$ es

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

Nuestro modelo estimado es entonces

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

Una vez estimado el parámetro, podemos utilizar el modelo para realizar predicciones probabilísticas.

Por ejemplo, la probabilidad de recibir exactamente ocho llamadas durante una hora es

$$
P(X=8)
=
e^{-5}\frac{5^8}{8!}.
$$

```python
import math

lam = lambda_estimado
k = 8

probabilidad = math.exp(-lam) * lam**k / math.factorial(k)

print("P(X = 8) =", probabilidad)
```

El proceso completo puede resumirse como

$$
\boxed{
\text{datos}
\longrightarrow
\text{estimación de }\lambda
\longrightarrow
\text{modelo}
\longrightarrow
\text{predicción probabilística}.
}
$$

<br><br>

## 8. Simulación de modelos de Poisson

La simulación computacional permite estudiar el comportamiento de un modelo estocástico y compararlo con sus propiedades teóricas.

<br><br>

### 8.1. Simulación de una distribución de Poisson

Supongamos que

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

Teóricamente,

$$
E[X]=5
$$

y

$$
\operatorname{Var}(X)=5.
$$

Por tanto, esperamos encontrar aproximadamente

$$
\overline X\approx5
$$

y

$$
s^2\approx5.
$$

Al aumentar el número de simulaciones, estos valores deberían aproximarse cada vez más a los valores teóricos.

<br><br>

### 8.2. Comparación entre simulación y modelo

Podemos comparar la distribución empírica obtenida mediante simulación con la distribución teórica.

```python
import numpy as np
import matplotlib.pyplot as plt
import math

lam = 5
n = 10000

datos = np.random.poisson(lam, size=n)

valores = np.arange(0, datos.max() + 1)

probabilidades = [
    math.exp(-lam) * lam**k / math.factorial(k)
    for k in valores
]

plt.hist(
    datos,
    bins=np.arange(-0.5, datos.max() + 1.5),
    density=True,
    alpha=0.6
)

plt.plot(valores, probabilidades, "o")

plt.xlabel("Número de eventos")
plt.ylabel("Probabilidad")
plt.title("Modelo de Poisson y simulación")
plt.show()
```

La distribución obtenida mediante simulación debería aproximarse a la distribución teórica.

La discrepancia observada se debe a que una simulación representa solamente una muestra finita.

<br><br>

### 8.3. Simulación de un proceso de Poisson

Para simular directamente un proceso de Poisson podemos utilizar la relación con la distribución exponencial.

Si la tasa es $\lambda$, los tiempos entre eventos

$$
T_1,T_2,T_3,\ldots
$$

son variables aleatorias independientes con distribución exponencial:

$$
T_i\sim\operatorname{Exponencial}(\lambda).
$$

Los tiempos acumulados de ocurrencia son

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
S_n=\sum_{i=1}^{n}T_i.
$$

Cada $S_n$ representa el instante en que ocurre el evento $n$.

Podemos simular este proceso mediante:

```python
import numpy as np

lam = 3
tiempo_maximo = 10

tiempos_eventos = []

tiempo = 0

while tiempo < tiempo_maximo:
    
    espera = np.random.exponential(1 / lam)
    tiempo += espera
    
    if tiempo < tiempo_maximo:
        tiempos_eventos.append(tiempo)

print(tiempos_eventos)
```

Podemos visualizar los tiempos de ocurrencia:

```python
import matplotlib.pyplot as plt

plt.eventplot(tiempos_eventos)

plt.xlabel("Tiempo")
plt.yticks([])
plt.title("Simulación de un proceso de Poisson")

plt.show()
```

Los eventos no aparecen separados por intervalos regulares. Algunos pueden ocurrir muy cerca unos de otros, mientras que entre otros puede existir un intervalo relativamente largo.

Esto permite visualizar una diferencia importante entre un modelo determinista y un modelo estocástico.

En un modelo determinista podríamos especificar exactamente los tiempos de ocurrencia. En un proceso de Poisson, en cambio, solamente conocemos la distribución de dichos tiempos.

<br><br>

## 9. Aplicaciones de los modelos de Poisson

Los modelos de Poisson pueden utilizarse en una gran variedad de problemas en los cuales interesa contar eventos.

<br><br>

### 9.1. Llegada de clientes

Supongamos que un establecimiento recibe clientes a una tasa promedio de

$$
\lambda=12
$$

clientes por hora.

Entonces, bajo los supuestos del modelo,

$$
N(t)\sim\operatorname{Poisson}(12t).
$$

Podemos utilizar el modelo para calcular probabilidades asociadas con diferentes intervalos de tiempo.

<br><br>

### 9.2. Llamadas telefónicas

Una central telefónica puede recibir llamadas aproximadamente de manera independiente y a una tasa promedio determinada.

Si la tasa es

$$
\lambda=20
$$

llamadas por hora, entonces el número de llamadas durante treinta minutos puede modelarse mediante

$$
N(0.5)\sim\operatorname{Poisson}(10).
$$

<br><br>

### 9.3. Fallas de componentes

Supongamos que un sistema registra en promedio

$$
\lambda=2
$$

fallas por día.

Si las fallas pueden considerarse aproximadamente independientes y la tasa es estable, podemos utilizar

$$
N(t)\sim\operatorname{Poisson}(2t)
$$

para representar el número de fallas durante $t$ días.

<br><br>

### 9.4. Defectos de fabricación

Supongamos que una determinada clase de material presenta, en promedio, cuatro defectos por cada cien metros.

Si $X$ representa el número de defectos encontrados en cien metros, podemos plantear

$$
X\sim\operatorname{Poisson}(4).
$$

Para una longitud de $200$ metros, el número esperado de defectos sería

$$
\lambda=8,
$$

por lo que

$$
X\sim\operatorname{Poisson}(8).
$$

<br><br>

### 9.5. Eventos biológicos

En determinados modelos simplificados de genética, el número de mutaciones observadas en una región puede modelarse mediante una distribución de Poisson.

Por ejemplo, si el número esperado de mutaciones en una región determinada es

$$
\lambda=3,
$$

podemos utilizar

$$
X\sim\operatorname{Poisson}(3)
$$

para representar el número de mutaciones observadas.

Es importante señalar que la distribución de Poisson no debe utilizarse automáticamente cada vez que una variable representa un conteo. La elección del modelo depende de los mecanismos que generan los eventos y de los supuestos que podamos considerar razonables.

<br><br>

## 10. ¿Cuándo es razonable utilizar un modelo de Poisson?

El modelo de Poisson es particularmente apropiado cuando estamos interesados en contar eventos que ocurren durante un intervalo de tiempo o dentro de una región espacial y cuando podemos considerar razonables determinados supuestos.

Entre ellos se encuentran:

* los eventos ocurren individualmente;
* los eventos pueden considerarse independientes;
* existe una tasa promedio de ocurrencia aproximadamente constante;
* la probabilidad de que ocurran varios eventos exactamente al mismo tiempo es muy pequeña;
* el número de eventos en intervalos disjuntos puede considerarse independiente.

Estos supuestos constituyen una idealización del fenómeno real.

Por ejemplo, supongamos que una tienda recibe clientes con una tasa promedio de $10$ clientes por hora durante la mañana y $30$ clientes por hora durante la tarde.

En este caso, utilizar una única tasa constante

$$
\lambda=20
$$

durante todo el día podría ser una mala representación del fenómeno.

Podría ser más apropiado considerar una tasa dependiente del tiempo:

$$
\lambda=\lambda(t).
$$

Este tipo de modelo conduce a procesos de Poisson no homogéneos, que constituyen una extensión del modelo estudiado en este capítulo.

De manera similar, si la ocurrencia de un evento modifica significativamente la probabilidad de que ocurra el siguiente, el supuesto de independencia puede dejar de ser apropiado.

Por tanto, construir un modelo de Poisson no consiste simplemente en aplicar una fórmula. Es necesario analizar si las hipótesis del modelo son compatibles con el fenómeno que queremos representar.

<br><br>

## 11. Comparación con los modelos de Markov

Los modelos de Markov y los modelos de Poisson pertenecen ambos a la familia de modelos estocásticos, pero describen aspectos diferentes de un sistema.

En un modelo de Markov, el objeto principal es el **estado del sistema** y las probabilidades de transición entre estados.

Por ejemplo,

$$
X_0\rightarrow X_1\rightarrow X_2\rightarrow\cdots
$$

representa una evolución aleatoria en la cual el sistema cambia de estado.

En un modelo de Poisson, el objeto principal es el **número de eventos** que ocurren durante un intervalo:

$$
N(t)=\text{número de eventos ocurridos hasta el tiempo }t.
$$

Podemos resumir la diferencia mediante la siguiente tabla:

| Modelo                           | Objeto principal  | Pregunta                                               |
| -------------------------------- | ----------------- | ------------------------------------------------------ |
| Modelo discreto determinista     | Estado o cantidad | ¿Cómo cambia el sistema?                               |
| Modelo continuo determinista     | Estado o cantidad | ¿Cómo evoluciona continuamente?                        |
| Modelo de Markov                 | Estado aleatorio  | ¿En qué estado estará el sistema?                      |
| Modelo de Poisson                | Número de eventos | ¿Cuántos eventos ocurrirán?                            |
| Proceso de Poisson + exponencial | Eventos y tiempos | ¿Cuántos eventos ocurren y cuándo ocurre el siguiente? |

Los modelos de Markov y Poisson no deben entenderse como modelos que compiten entre sí. Son herramientas diferentes que pueden resultar apropiadas para diferentes tipos de fenómenos.

En particular, el modelo de Markov resulta natural cuando el concepto de **estado** es central, mientras que el modelo de Poisson resulta natural cuando el fenómeno puede describirse mediante la ocurrencia de **eventos**.

<br><br>

## 12. Ideas principales

En este capítulo estudiamos los modelos de Poisson como una herramienta para representar la ocurrencia aleatoria de eventos.

Las ideas fundamentales son:

1. La distribución binomial permite contar el número de éxitos en un número fijo de ensayos independientes.

2. La distribución de Poisson aparece como una aproximación de la distribución binomial cuando el número de ensayos es grande, la probabilidad de éxito es pequeña y

$$
np=\lambda
$$

permanece constante.

3. La distribución de Poisson está dada por

$$
\boxed{
P(X=k)
=
e^{-\lambda}
\frac{\lambda^k}{k!}.
}
$$

4. Para una variable de Poisson,

$$
\boxed{
E[X]=\lambda,
\qquad
\operatorname{Var}(X)=\lambda.
}
$$

5. En un proceso de Poisson con tasa $\lambda$,

$$
\boxed{
N(t)\sim\operatorname{Poisson}(\lambda t).
}
$$

6. $\lambda$ representa una tasa de ocurrencia, mientras que $\lambda t$ representa el número esperado de eventos durante un intervalo de duración $t$.

7. La probabilidad de que ocurra al menos un evento durante un intervalo de duración $t$ es

$$
\boxed{
P(N(t)\geq1)=1-e^{-\lambda t}.
}
$$

8. Los tiempos entre eventos de un proceso de Poisson siguen una distribución exponencial.

9. Para datos provenientes de una distribución de Poisson, el estimador de máxima verosimilitud de $\lambda$ es

$$
\boxed{
\hat{\lambda}=\overline{x}.
}
$$

10. La simulación computacional permite generar realizaciones del modelo y comparar sus propiedades empíricas con las predicciones teóricas.

El modelo de Poisson constituye así una nueva herramienta dentro del repertorio de modelos matemáticos estudiados en este libro:

$$
\boxed{
\text{modelo}
\rightarrow
\text{supuestos}
\rightarrow
\text{parámetros}
\rightarrow
\text{predicción}
\rightarrow
\text{simulación}
}
$$

A diferencia de los modelos deterministas estudiados anteriormente, el resultado de un modelo de Poisson no es una única trayectoria o un único valor. El modelo proporciona una descripción probabilística de los posibles resultados.

A su vez, a diferencia de los modelos de Markov, en los cuales el interés principal está en la evolución entre estados, los modelos de Poisson se concentran en la ocurrencia y el conteo de eventos.

<br><br>

## 13. Ejercicios

<br><br>

### 13.1. Distribución de Poisson

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

<br><br>

### 13.2. Llegada de clientes

Una cafetería recibe en promedio $8$ clientes por hora.

Suponga que las llegadas pueden modelarse mediante un proceso de Poisson.

a. ¿Cuál es el número esperado de clientes durante tres horas?

b. ¿Cuál es la probabilidad de que lleguen exactamente $20$ clientes durante tres horas?

c. ¿Cuál es la probabilidad de que no llegue ningún cliente durante treinta minutos?

d. ¿Cuál es la probabilidad de que llegue al menos un cliente durante treinta minutos?

<br><br>

### 13.3. Llamadas telefónicas

Una central recibe en promedio $12$ llamadas por hora.

a. Construya un modelo de Poisson para el número de llamadas recibidas durante una hora.

b. Calcule la probabilidad de recibir exactamente $15$ llamadas.

c. Calcule la probabilidad de recibir más de $15$ llamadas.

d. Calcule la probabilidad de no recibir llamadas durante los próximos diez minutos.

<br><br>

### 13.4. Estimación de $\lambda$

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

<br><br>

### 13.5. Simulación

Utilice Python para generar $10,000$ observaciones de

$$
X\sim\operatorname{Poisson}(\lambda)
$$

para

$$
\lambda=1,\qquad
\lambda=5,\qquad
\lambda=10,\qquad
\lambda=20.
$$

Para cada caso:

a. calcule la media muestral;

b. calcule la varianza muestral;

c. compare estos valores con la media y la varianza teóricas;

d. construya la distribución empírica;

e. analice cómo cambia la forma de la distribución cuando aumenta $\lambda$.

<br><br>

### 13.6. Proceso de Poisson

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

<br><br>

### 13.7. Binomial y Poisson

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

<br><br>

### 13.8. Evaluación de un modelo

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

<br><br>

### 13.9. Proyecto computacional

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

1. Defina claramente el evento que será contado.
2. Especifique la unidad temporal o espacial utilizada.
3. Estime el parámetro $\lambda$.
4. Construya el modelo de Poisson.
5. Calcule algunas probabilidades de interés.
6. Simule observaciones mediante Python.
7. Compare los datos observados con los datos simulados.
8. Discuta las hipótesis necesarias para que el modelo sea razonable.
9. Indique posibles limitaciones del modelo.

El propósito del ejercicio no es solamente obtener un valor para $\lambda$, sino recorrer el proceso completo de construcción, análisis y evaluación de un modelo estocástico.
