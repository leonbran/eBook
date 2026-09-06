# Construcción de modelos por ajuste a datos

La construcción de modelos matemáticos puede comenzar de diferentes maneras. En algunos casos, el modelo surge de principios físicos, químicos o biológicos que permiten establecer ecuaciones a partir de leyes fundamentales. En otros casos, disponemos principalmente de **datos experimentales u observacionales** y queremos identificar una relación matemática que permita describir, interpretar y predecir el comportamiento observado.

En este capítulo estudiaremos una de las herramientas más importantes para construir modelos a partir de datos: la **regresión lineal**.

La idea fundamental es sencilla. Supongamos que tenemos un conjunto de observaciones

$$
\{(x_i,y_i)\}_{i=1}^n,
$$

donde $x_i$ representa una variable que consideramos explicativa y $y_i$ una variable de respuesta. Nuestro objetivo es encontrar una función

$$
y\approx f(x)
$$

que describa razonablemente la relación observada entre ambas variables.

La función $f$ constituye entonces un **modelo matemático de los datos**.

En el caso más sencillo podemos proponer una función lineal

$$
f(x)=mx+b.
$$

Los parámetros $m$ y $b$ se determinan a partir de los datos mediante el método de **mínimos cuadrados**.

La importancia de la regresión lineal va mucho más allá de encontrar una recta. El método de mínimos cuadrados constituye una herramienta fundamental para construir una gran variedad de modelos matemáticos. Incluso cuando la relación entre las variables no es directamente lineal, podemos transformar las variables, utilizar diferentes funciones base o dividir el dominio en regiones para construir modelos más adecuados.

Por esta razón, en este capítulo utilizaremos la regresión lineal como una de las herramientas centrales para pasar de los **datos** a un **modelo matemático**.

El proceso general puede representarse como

$$
\boxed{
\text{datos}
\longrightarrow
\text{patrón}
\longrightarrow
\text{modelo}
\longrightarrow
\text{predicción}
\longrightarrow
\text{validación}.
}
$$

En este proceso también encontraremos otra herramienta importante: la **interpolación**. A diferencia de la regresión, cuyo objetivo es encontrar un modelo que se aproxime a los datos, la interpolación busca construir una función que pase exactamente por los datos conocidos.

<br>

## 1. La regresión lineal como herramienta para construir modelos

Supongamos que tenemos un conjunto de datos

$$
\{(x_i,y_i)\}_{i=1}^{n}.
$$

Una primera pregunta que podemos hacernos es:

> ¿Existe una relación aproximadamente lineal entre $x$ y $y$?

Si la respuesta es afirmativa, podemos proponer

$$
y\approx mx+b.
$$

La regresión lineal permite determinar los valores de $m$ y $b$ que proporcionan el mejor ajuste posible según el criterio de mínimos cuadrados.

Pero la importancia de esta idea no termina allí.

La regresión lineal puede utilizarse para construir diferentes modelos mediante transformaciones. Por ejemplo:

### Modelo lineal

$$
y=a+bx.
$$

### Modelo cuadrático

$$
y=a+bx+cx^2.
$$

### Modelo polinomial

$$
y=a_0+a_1x+a_2x^2+\cdots+a_kx^k.
$$

### Modelo exponencial

$$
y=Ae^{kx}.
$$

Tomando logaritmos:

$$
\ln y=\ln A+kx,
$$

obtenemos una relación lineal entre $\ln y$ y $x$.

### Modelo de potencias

$$
y=Ax^p.
$$

Tomando logaritmos:

$$
\ln y=\ln A+p\ln x.
$$

De nuevo obtenemos una relación lineal.

Así, la regresión lineal constituye una herramienta fundamental para construir modelos con diferentes formas matemáticas.

La idea central puede resumirse como

$$
\boxed{
\text{regresión lineal}
\quad\Longrightarrow\quad
\text{familia de modelos ajustados a datos}.
}
$$

<br>

## 2. Fundamentos matemáticos: regresión lineal por mínimos cuadrados

### 2.1 El modelo lineal

Consideremos un conjunto de $n$ pares de datos

$$
\{(x_i,y_i)\}_{i=1}^{n}
=
\{(x_1,y_1),(x_2,y_2),\ldots,(x_n,y_n)\}.
$$

Queremos construir un modelo de la forma

$$
f(x)=mx+b,
$$

donde:

- $x$ es la variable independiente o explicativa;
- $y$ es la variable dependiente o de respuesta;
- $m$ es la pendiente;
- $b$ es la intersección con el eje $y$.

El modelo propone que

$$
y_i\approx mx_i+b.
$$

El valor que predice el modelo para $x_i$ es

$$
\hat y_i=mx_i+b.
$$

La diferencia entre el valor observado y el valor predicho es

$$
e_i=y_i-\hat y_i.
$$

Esta cantidad se denomina **residuo**.

> **Definición — Residuo**
>
> Para una observación $(x_i,y_i)$, el residuo asociado al modelo $\hat y=f(x)$ es
>
> $$
> e_i=y_i-f(x_i).
> $$
>
> El residuo mide la diferencia entre el valor observado y el valor predicho por el modelo.

<br>

### 2.2 El criterio de mínimos cuadrados

Existen infinitas rectas que podemos utilizar para aproximar los datos. Necesitamos entonces establecer un criterio para determinar cuál es la "mejor".

El método de mínimos cuadrados define la función

$$
E(m,b)
=
\sum_{i=1}^{n}
\left(y_i-(mx_i+b)\right)^2.
$$

Esta cantidad representa la suma de los cuadrados de los residuos.

El objetivo es encontrar los valores de $m$ y $b$ que minimizan esta cantidad:

$$
\boxed{
(\hat m,\hat b)
=
\underset{m,b}{\operatorname{argmin}}
\;
\sum_{i=1}^{n}
\left(y_i-(mx_i+b)\right)^2
}
$$

Como se trata de una suma de cuadrados,

$$
E(m,b)\geq0.
$$

Además,

$$
E(m,b)=0
$$

si y solamente si todos los puntos se encuentran exactamente sobre la recta.

<br>

### 2.3 Interpretación geométrica

Cada dato $(x_i,y_i)$ puede compararse con el punto correspondiente sobre la recta,

$$
(x_i,\hat y_i).
$$

La diferencia vertical es

$$
y_i-\hat y_i=e_i.
$$

El método de mínimos cuadrados busca minimizar

$$
e_1^2+e_2^2+\cdots+e_n^2.
$$

Por tanto, la recta de regresión puede interpretarse como la recta que minimiza la suma de los cuadrados de las diferencias verticales entre los datos observados y los valores predichos.

<br>

## 3. Teorema de regresión lineal por mínimos cuadrados

> **Teorema — Regresión lineal por mínimos cuadrados**
>
> Sea
>
> $$
> \{(x_i,y_i)\}_{i=1}^n
> $$
>
> un conjunto de datos con $n\geq2$, y supongamos que no todos los valores $x_i$ son iguales. Consideremos el modelo
>
> $$
> f(x)=mx+b.
> $$
>
> Entonces, los valores de $m$ y $b$ que minimizan
>
> $$
> E(m,b)=
> \sum_{i=1}^{n}(y_i-mx_i-b)^2
> $$
>
> están dados por
>
> $$
> \boxed{
> \hat m=
> \frac{
> n\displaystyle\sum_{i=1}^{n}x_i y_i
> -
> \left(\displaystyle\sum_{i=1}^{n}x_i\right)
> \left(\displaystyle\sum_{i=1}^{n}y_i\right)
> }{
> n\displaystyle\sum_{i=1}^{n}x_i^2
> -
> \left(\displaystyle\sum_{i=1}^{n}x_i\right)^2
> }
> }
> $$
>
> y
>
> $$
> \boxed{
> \hat b=
> \frac{1}{n}
> \left(
> \sum_{i=1}^{n}y_i
> -
> \hat m\sum_{i=1}^{n}x_i
> \right).
> }
> $$

<br>

### 3.1 Demostración

Consideremos

$$
E(m,b)
=
\sum_{i=1}^{n}
(y_i-mx_i-b)^2.
$$

Para encontrar el mínimo derivamos parcialmente respecto a $m$ y $b$.

Respecto a $m$:

$$
\frac{\partial E}{\partial m}
=
-2
\sum_{i=1}^{n}
x_i(y_i-mx_i-b).
$$

Igualando a cero:

$$
\sum_{i=1}^{n}x_i y_i
-
m\sum_{i=1}^{n}x_i^2
-
b\sum_{i=1}^{n}x_i
=0.
$$

Por tanto,

$$
\sum_{i=1}^{n}x_i y_i
=
m\sum_{i=1}^{n}x_i^2
+
b\sum_{i=1}^{n}x_i.
$$

Respecto a $b$:

$$
\frac{\partial E}{\partial b}
=
-2
\sum_{i=1}^{n}
(y_i-mx_i-b).
$$

Igualando a cero:

$$
\sum_{i=1}^{n}y_i
-
m\sum_{i=1}^{n}x_i
-
bn
=0.
$$

Por tanto,

$$
\sum_{i=1}^{n}y_i
=
m\sum_{i=1}^{n}x_i+bn.
$$

Estas dos ecuaciones se conocen como las **ecuaciones normales**:

$$
\begin{cases}
\displaystyle
\sum x_i y_i
=
m\sum x_i^2+b\sum x_i,
\\[1em]
\displaystyle
\sum y_i
=
m\sum x_i+bn.
\end{cases}
$$

De la segunda ecuación,

$$
b=
\frac{
\sum y_i-m\sum x_i
}{n}.
$$

Sustituyendo en la primera:

$$
\sum x_i y_i
=
m\sum x_i^2
+
\left(
\frac{\sum y_i-m\sum x_i}{n}
\right)
\sum x_i.
$$

Multiplicando por $n$:

$$
n\sum x_i y_i
=
mn\sum x_i^2
+
\left(\sum y_i-m\sum x_i\right)
\sum x_i.
$$

Entonces,

$$
n\sum x_i y_i
=
mn\sum x_i^2
+
\left(\sum x_i\right)
\left(\sum y_i\right)
-
m\left(\sum x_i\right)^2.
$$

Agrupando los términos que contienen $m$:

$$
n\sum x_i y_i
-
\left(\sum x_i\right)
\left(\sum y_i\right)
=
m
\left[
n\sum x_i^2
-
\left(\sum x_i\right)^2
\right].
$$

Finalmente,

$$
\boxed{
\hat m=
\frac{
n\sum x_i y_i
-
(\sum x_i)(\sum y_i)
}{
n\sum x_i^2-(\sum x_i)^2
}.
}
$$

Una vez obtenida la pendiente,

$$
\boxed{
\hat b=
\frac{
\sum y_i-\hat m\sum x_i
}{n}.
}
$$

<br>

## 4. Una formulación conveniente de la recta de regresión

Definamos los valores medios

$$
\bar x=\frac{1}{n}\sum_{i=1}^n x_i,
\qquad
\bar y=\frac{1}{n}\sum_{i=1}^n y_i.
$$

La pendiente puede escribirse como

$$
\boxed{
\hat m=
\frac{
\displaystyle\sum_{i=1}^{n}
(x_i-\bar x)(y_i-\bar y)
}{
\displaystyle\sum_{i=1}^{n}
(x_i-\bar x)^2
}.
}
$$

El intercepto es

$$
\boxed{
\hat b=\bar y-\hat m\bar x.
}
$$

Por tanto,

$$
\boxed{
\hat y=\hat m(x-\bar x)+\bar y.
}
$$

Esta expresión permite observar una propiedad geométrica importante:

> **La recta de regresión por mínimos cuadrados siempre pasa por el punto $(\bar x,\bar y)$.**

<br>

## 5. Interpretación de los parámetros

Una vez obtenido

$$
\hat y=\hat m x+\hat b,
$$

debemos interpretar los parámetros dentro del contexto del problema.

### 5.1 La pendiente

La pendiente $\hat m$ representa el cambio promedio esperado en $y$ asociado a un incremento de una unidad en $x$.

Si

$$
\hat m>0,
$$

el modelo representa una tendencia creciente.

Si

$$
\hat m<0,
$$

representa una tendencia decreciente.

La interpretación debe considerar siempre las unidades.

Por ejemplo, si $x$ está medido en horas y $y$ en metros, entonces la pendiente tiene unidades

$$
\frac{\text{metros}}{\text{hora}}.
$$

<br>

### 5.2 El intercepto

El intercepto $\hat b$ representa el valor predicho cuando

$$
x=0.
$$

Pero no siempre tiene significado físico.

Si los datos fueron recolectados únicamente para

$$
10\leq x\leq20,
$$

entonces $x=0$ se encuentra fuera del rango de observación.

En ese caso, el intercepto puede ser matemáticamente necesario para definir el modelo, pero su interpretación física puede carecer de sentido.

<br>

## 6. Ejemplo: relación entre nutrientes y crecimiento bacteriano

Supongamos que un biólogo estudia la relación entre la concentración de nutrientes disponible en un medio y el tamaño de una población bacteriana.

Se obtienen los siguientes datos:

| Concentración de nutrientes $x$ (mg/L) | Población bacteriana $y$ |
|---:|---:|
| 1 | 20000 |
| 2 | 25000 |
| 3 | 35000 |
| 4 | 40000 |
| 5 | 45000 |
| 6 | 50000 |

Queremos construir un modelo que describa la relación entre ambas variables.

<br>

### 6.1 Visualización

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.array([1, 2, 3, 4, 5, 6])
y = np.array([20000, 25000, 35000, 40000, 45000, 50000])

plt.scatter(x, y)

plt.xlabel("Concentración de nutrientes (mg/L)")
plt.ylabel("Población bacteriana")
plt.title("Nutrientes vs. población bacteriana")

plt.show()
```

La gráfica muestra una tendencia creciente que parece aproximadamente lineal.

Esto no demuestra que el modelo lineal sea correcto, pero proporciona una primera hipótesis.

<br>

### 6.2 Ajuste de la recta

Calculamos primero los promedios:

```python
x_mean = np.mean(x)
y_mean = np.mean(y)
```

Luego calculamos la pendiente:

```python
m = np.sum((x - x_mean) * (y - y_mean)) / np.sum((x - x_mean)**2)
```

y el intercepto:

```python
b = y_mean - m * x_mean
```

Obtenemos aproximadamente

$$
\hat m=6142.86
$$

y

$$
\hat b=14333.33.
$$

Por tanto,

$$
\boxed{
\hat y=6142.86x+14333.33.
}
$$

<br>

### 6.3 Interpretación

La pendiente indica que, según el modelo, un aumento de $1$ mg/L en la concentración de nutrientes está asociado con un aumento promedio de aproximadamente

$$
6143
$$

bacterias.

El intercepto es aproximadamente

$$
14333.
$$

Matemáticamente, este es el valor predicho para $x=0$. Sin embargo, como nuestros datos comienzan en $x=1$, debemos ser cuidadosos al darle una interpretación física.

<br>

### 6.4 Cálculo de $R^2$

El coeficiente de determinación se define como

$$
R^2
=
1-
\frac{
\displaystyle\sum_{i=1}^n(y_i-\hat y_i)^2
}{
\displaystyle\sum_{i=1}^n(y_i-\bar y)^2
}.
$$

En Python:

```python
y_pred = m * x + b

SSE = np.sum((y - y_pred)**2)
SST = np.sum((y - np.mean(y))**2)

R2 = 1 - SSE / SST

print("R^2 =", R2)
```

Para estos datos obtenemos aproximadamente

$$
\boxed{
R^2\approx0.9844.
}
$$

Esto indica que el modelo lineal explica una proporción muy alta de la variabilidad observada.

Sin embargo, un valor elevado de $R^2$ no es suficiente para determinar si el modelo es apropiado. También debemos examinar los residuos y el contexto del fenómeno.

<br>

### 6.5 Predicción

Para una concentración de

$$
x=5.5\text{ mg/L},
$$

el modelo predice

$$
\hat y
=
6142.86(5.5)+14333.33
\approx48119.
$$

En Python:

```python
x_nuevo = 5.5

y_nuevo = m * x_nuevo + b

print("Predicción:", y_nuevo)
```

Como $5.5$ se encuentra dentro del rango observado $[1,6]$, estamos realizando una predicción dentro del intervalo de los datos.

<br>

## 7. Residuos y evaluación del ajuste

Una vez construido el modelo,

$$
\hat y_i=\hat m x_i+\hat b,
$$

podemos calcular los residuos:

$$
e_i=y_i-\hat y_i.
$$

En Python:

```python
residuos = y - y_pred

print(residuos)
```

Podemos visualizarlos:

```python
plt.scatter(x, residuos)

plt.axhline(0, linestyle="--")

plt.xlabel("Concentración de nutrientes (mg/L)")
plt.ylabel("Residuo")
plt.title("Residuos de la regresión lineal")

plt.show()
```

La pregunta fundamental es:

> ¿Los residuos se distribuyen aproximadamente de manera aleatoria alrededor de cero?

Si observamos patrones sistemáticos, puede ser una señal de que la forma lineal del modelo no es adecuada.

Por ejemplo, si los residuos presentan una estructura como

$$
-,\quad 0,\quad +,\quad +,\quad 0,\quad -,
$$

podría existir una relación curva que el modelo lineal no está capturando.

El análisis de residuos constituye, por tanto, una parte importante del proceso de construcción y validación de un modelo.

<br>

## 8. Construcción de otros modelos mediante regresión lineal

La regresión lineal no debe entenderse únicamente como el ajuste de una recta.

Una idea mucho más general consiste en escribir un modelo como

$$
y
=
\beta_0\phi_0(x)
+
\beta_1\phi_1(x)
+\cdots+
\beta_k\phi_k(x),
$$

donde

$$
\phi_0,\phi_1,\ldots,\phi_k
$$

son funciones conocidas y los parámetros

$$
\beta_0,\beta_1,\ldots,\beta_k
$$

son desconocidos.

El modelo sigue siendo **lineal en los parámetros**, aunque no necesariamente sea una recta en $x$.

Esta idea permite utilizar mínimos cuadrados para construir modelos mucho más generales.

<br>

### 8.1 Modelos polinomiales

Por ejemplo,

$$
y=\beta_0+\beta_1x+\beta_2x^2
$$

es un modelo cuadrático.

También podemos considerar

$$
y=
\beta_0+\beta_1x+\beta_2x^2+\beta_3x^3.
$$

Aunque las gráficas son curvas, el modelo es lineal respecto a los parámetros $\beta_i$.

En Python:

```python
coeficientes = np.polyfit(x, y, 2)

print(coeficientes)
```

Esto permite construir modelos polinomiales mediante mínimos cuadrados.

<br>

### 8.2 Modelos exponenciales

Consideremos

$$
y=Ae^{kx}.
$$

Tomando logaritmos:

$$
\ln y=\ln A+kx.
$$

Si definimos

$$
Y=\ln y,
$$

entonces

$$
Y=\ln A+kx.
$$

Esto tiene la forma de una regresión lineal:

$$
Y=b+mx.
$$

Después del ajuste podemos recuperar los parámetros originales:

$$
k=m,
$$

y

$$
A=e^b.
$$

Por tanto, podemos utilizar regresión lineal para construir un modelo exponencial.

<br>

### 8.3 Modelos de potencias

Consideremos ahora

$$
y=Ax^p.
$$

Tomando logaritmos:

$$
\ln y=\ln A+p\ln x.
$$

Definiendo

$$
X=\ln x,
\qquad
Y=\ln y,
$$

obtenemos

$$
Y=\ln A+pX.
$$

Nuevamente tenemos un problema de regresión lineal.

Este procedimiento permite construir modelos de leyes de potencia a partir de datos.

<br>

## 9. Cuando una sola función no describe adecuadamente los datos

No siempre es posible representar adecuadamente todos los datos mediante una única función sencilla.

Supongamos que tenemos los datos

| $x$ | $y$ |
|---:|---:|
| 0 | 2 |
| 1 | 5 |
| 2 | 8 |
| 3 | 11 |
| 4 | 14 |
| 5 | 15 |
| 6 | 14 |
| 7 | 11 |
| 8 | 8 |
| 9 | 5 |
| 10 | 2 |

Al observar estos datos encontramos una característica importante.

Para

$$
0\leq x\leq5,
$$

la variable $y$ aumenta.

Pero para

$$
5\leq x\leq10,
$$

la variable $y$ disminuye.

Por tanto, una única recta no describe adecuadamente todo el conjunto de datos.

La gráfica tendría aproximadamente la forma de una "montaña".

<br>

### 9.1 ¿Qué significa que la relación no sea biyectiva?

Recordemos que una función

$$
f:X\longrightarrow Y
$$

es biyectiva si es simultáneamente inyectiva y sobreyectiva.

En el contexto de los datos, podemos encontrarnos con situaciones en las que distintos valores de $x$ producen el mismo valor de $y$.

Por ejemplo,

$$
y(4)=14,
\qquad
y(6)=14.
$$

Por tanto, la relación completa no puede interpretarse como una función invertible $x\mapsto y$.

Sin embargo, esto **no impide** construir un modelo $y=f(x)$.

Lo que sí puede ocurrir es que una única función sencilla no represente adecuadamente toda la estructura de los datos.

Una estrategia consiste en **dividir el dominio en regiones** y construir un modelo diferente en cada región.

<br>

### 9.2 División del dominio

En nuestro ejemplo podemos dividir los datos en dos regiones:

$$
0\leq x\leq5
$$

y

$$
5\leq x\leq10.
$$

En la primera región tenemos una tendencia creciente.

En la segunda tenemos una tendencia decreciente.

Por tanto, podemos proponer

$$
f(x)=
\begin{cases}
f_1(x), & 0\leq x\leq5,\\
f_2(x), & 5\leq x\leq10.
\end{cases}
$$

Ahora ajustaremos una recta a cada conjunto de datos.

<br>

### 9.3 Ajuste de la primera región

Consideramos

$$
x_1=(0,1,2,3,4,5)
$$

y

$$
y_1=(2,5,8,11,14,15).
$$

Podemos utilizar `polyfit`:

```python
x1 = np.array([0, 1, 2, 3, 4, 5])
y1 = np.array([2, 5, 8, 11, 14, 15])

m1, b1 = np.polyfit(x1, y1, 1)

print("m1 =", m1)
print("b1 =", b1)
```

Obtenemos aproximadamente

$$
m_1=2.7143,
$$

y

$$
b_1=2.3810.
$$

Por tanto,

$$
\boxed{
f_1(x)=2.7143x+2.3810.
}
$$

<br>

### 9.4 Ajuste de la segunda región

Ahora consideramos

$$
x_2=(5,6,7,8,9,10)
$$

y

$$
y_2=(15,14,11,8,5,2).
$$

```python
x2 = np.array([5, 6, 7, 8, 9, 10])
y2 = np.array([15, 14, 11, 8, 5, 2])

m2, b2 = np.polyfit(x2, y2, 1)

print("m2 =", m2)
print("b2 =", b2)
```

Obtenemos aproximadamente

$$
m_2=-2.7143,
$$

y

$$
b_2=29.5238.
$$

Por tanto,

$$
\boxed{
f_2(x)=-2.7143x+29.5238.
}
$$

<br>

### 9.5 Modelo por tramos

El modelo completo queda entonces

$$
\boxed{
f(x)=
\begin{cases}
2.7143x+2.3810,
&0\leq x\leq5,
\\[0.5em]
-2.7143x+29.5238,
&5\leq x\leq10.
\end{cases}
}
$$

Hemos construido un modelo mediante **dos regresiones lineales diferentes**.

Esto se conoce como un **modelo por tramos**.

<br>

### 9.6 Visualización

```python
x = np.array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
y = np.array([2, 5, 8, 11, 14, 15, 14, 11, 8, 5, 2])

x1 = x[x <= 5]
x2 = x[x >= 5]

y1 = y[x <= 5]
y2 = y[x >= 5]

m1, b1 = np.polyfit(x1, y1, 1)
m2, b2 = np.polyfit(x2, y2, 1)

y1_pred = m1 * x1 + b1
y2_pred = m2 * x2 + b2

plt.scatter(x, y, label="Datos")

plt.plot(x1, y1_pred, label="Modelo 1")
plt.plot(x2, y2_pred, label="Modelo 2")

plt.xlabel("x")
plt.ylabel("y")
plt.legend()

plt.show()
```

Este ejemplo ilustra una idea fundamental:

> **Cuando una única función no representa adecuadamente los datos, podemos dividir el dominio en regiones y construir modelos diferentes para cada región.**

<br>

### 9.7 Continuidad del modelo

En algunos problemas queremos que las funciones por tramos coincidan en el punto donde se realiza la división.

En nuestro ejemplo, ambas rectas no necesariamente coinciden exactamente en $x=5$, debido a que fueron ajustadas independientemente.

En otros problemas podemos imponer la condición

$$
f_1(c)=f_2(c),
$$

donde $c$ es el punto de unión.

En ese caso obtenemos un modelo continuo:

$$
f(x)=
\begin{cases}
f_1(x),&x\leq c,\\
f_2(x),&x>c.
\end{cases}
$$

Dependiendo del problema, también puede ser necesario exigir continuidad de la derivada:

$$
f_1'(c)=f_2'(c).
$$

Esto conduce a modelos por tramos más suaves y constituye una idea importante en interpolación mediante *splines*.

<br>

## 10. Interpolación

La regresión no es la única manera de construir una función a partir de datos.

Supongamos que conocemos exactamente los puntos

$$
(x_1,y_1),\ldots,(x_n,y_n).
$$

En regresión buscamos una función que se aproxime a los datos:

$$
f(x_i)\approx y_i.
$$

En interpolación buscamos una función que pase exactamente por ellos:

$$
\boxed{
f(x_i)=y_i
\qquad
\text{para }i=1,\ldots,n.
}
$$

Esta es la diferencia fundamental.

### Regresión

$$
f(x_i)\approx y_i.
$$

### Interpolación

$$
f(x_i)=y_i.
$$

La interpolación resulta particularmente útil cuando conocemos valores exactos de una función en determinados puntos y queremos estimar los valores intermedios.

<br>

## 11. Interpolación lineal

La forma más sencilla de interpolación consiste en unir dos puntos mediante una recta.

Supongamos que conocemos

$$
(x_0,y_0)
$$

y

$$
(x_1,y_1).
$$

La recta que pasa por ellos es

$$
f(x)
=
y_0+
\frac{y_1-y_0}{x_1-x_0}
(x-x_0).
$$

Esta función satisface

$$
f(x_0)=y_0
$$

y

$$
f(x_1)=y_1.
$$

Por ejemplo, si conocemos

$$
(2,5)
$$

y

$$
(6,13),
$$

entonces

$$
f(x)
=
5+
\frac{13-5}{6-2}(x-2).
$$

Por tanto,

$$
f(x)=5+2(x-2),
$$

es decir,

$$
f(x)=2x+1.
$$

Para $x=4$ obtenemos

$$
f(4)=9.
$$

La interpolación lineal estima el valor intermedio mediante el segmento de recta que conecta los datos conocidos.

<br>

## 12. Interpolación polinomial

Si tenemos más de dos puntos, podemos buscar un polinomio que pase exactamente por todos ellos.

Dados $n$ puntos

$$
(x_1,y_1),\ldots,(x_n,y_n),
$$

con valores $x_i$ diferentes entre sí, existe un único polinomio de grado menor o igual que $n-1$ que satisface

$$
p(x_i)=y_i.
$$

Por ejemplo, con tres puntos podemos construir un polinomio cuadrático:

$$
p(x)=a+bx+cx^2.
$$

Los coeficientes se determinan imponiendo

$$
p(x_1)=y_1,
$$

$$
p(x_2)=y_2,
$$

y

$$
p(x_3)=y_3.
$$

<br>

## 13. Interpolación de Lagrange

Una de las formas más importantes de construir el polinomio interpolante es la **interpolación de Lagrange**.

Dados los puntos

$$
(x_1,y_1),\ldots,(x_n,y_n),
$$

definimos los polinomios base de Lagrange

$$
L_i(x)
=
\prod_{\substack{j=1\\j\neq i}}^n
\frac{x-x_j}{x_i-x_j}.
$$

Estos polinomios tienen la propiedad fundamental

$$
L_i(x_j)=
\begin{cases}
1,&i=j,\\
0,&i\neq j.
\end{cases}
$$

El polinomio interpolante es entonces

$$
\boxed{
p(x)=
\sum_{i=1}^{n}
y_iL_i(x).
}
$$

Gracias a la propiedad anterior,

$$
p(x_k)
=
\sum_{i=1}^{n}
y_iL_i(x_k).
$$

Todos los términos desaparecen excepto el correspondiente a $i=k$, por lo que

$$
p(x_k)=y_k.
$$

Así, el polinomio pasa exactamente por todos los puntos.

<br>

### 13.1 Ejemplo de interpolación de Lagrange

Consideremos los tres puntos

$$
(0,1),
\qquad
(1,3),
\qquad
(2,2).
$$

Tenemos

$$
L_1(x)
=
\frac{(x-1)(x-2)}
{(0-1)(0-2)}
=
\frac{(x-1)(x-2)}{2},
$$

$$
L_2(x)
=
\frac{(x-0)(x-2)}
{(1-0)(1-2)}
=
-x(x-2),
$$

y

$$
L_3(x)
=
\frac{(x-0)(x-1)}
{(2-0)(2-1)}
=
\frac{x(x-1)}{2}.
$$

Por tanto,

$$
p(x)
=
1L_1(x)
+
3L_2(x)
+
2L_3(x).
$$

Es decir,

$$
p(x)
=
\frac{(x-1)(x-2)}{2}
-
3x(x-2)
+
x(x-1).
$$

Simplificando:

$$
\boxed{
p(x)=
-\frac32x^2+\frac72x+1.
}
$$

Podemos verificar:

$$
p(0)=1,
$$

$$
p(1)=3,
$$

y

$$
p(2)=2.
$$

El polinomio reproduce exactamente los tres datos.

<br>

### 13.2 Interpolación de Lagrange en Python

Podemos construir el polinomio utilizando `scipy`:

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy.interpolate import lagrange

x = np.array([0, 1, 2])
y = np.array([1, 3, 2])

polinomio = lagrange(x, y)

x_nuevo = np.linspace(0, 2, 200)
y_nuevo = polinomio(x_nuevo)

plt.scatter(x, y, label="Datos")
plt.plot(x_nuevo, y_nuevo, label="Interpolación de Lagrange")

plt.xlabel("x")
plt.ylabel("y")
plt.legend()

plt.show()
```

También podemos evaluar el polinomio en cualquier punto dentro del intervalo.

Por ejemplo:

```python
valor = polinomio(1.5)

print(valor)
```

<br>

## 14. Regresión e interpolación: ¿cuál es la diferencia?

Regresión e interpolación utilizan datos para construir funciones, pero tienen objetivos diferentes.

### Regresión

En regresión buscamos una función que represente aproximadamente los datos:

$$
f(x_i)\approx y_i.
$$

Los datos pueden contener:

- errores experimentales;
- ruido;
- variabilidad natural;
- errores de medición.

Por ello, no esperamos necesariamente que el modelo pase exactamente por todos los puntos.

El objetivo es encontrar una función que represente adecuadamente la tendencia general.

<br>

### Interpolación

En interpolación suponemos que los datos conocidos deben ser reproducidos exactamente:

$$
f(x_i)=y_i.
$$

Por tanto, la función interpolante pasa por todos los puntos.

La interpolación es especialmente apropiada cuando:

- los datos son considerados exactos;
- conocemos una función mediante valores tabulados;
- queremos estimar valores entre puntos conocidos;
- no buscamos suavizar el ruido experimental.

<br>

### Comparación

| Característica | Regresión | Interpolación |
|---|---|---|
| Objetivo | Aproximar los datos | Reproducir exactamente los datos |
| ¿Pasa por todos los puntos? | No necesariamente | Sí |
| Maneja ruido | Sí | No necesariamente |
| Error en los datos | Permitido | Idealmente cero |
| Ejemplo | Mínimos cuadrados | Lagrange |
| Uso principal | Construcción de modelos | Estimación entre datos conocidos |

Podemos resumir la diferencia mediante

$$
\boxed{
\begin{aligned}
\text{Regresión:}&\qquad f(x_i)\approx y_i,\\[0.5em]
\text{Interpolación:}&\qquad f(x_i)=y_i.
\end{aligned}
}
$$

<br>

## 15. Interpolación y extrapolación

Es importante distinguir entre **interpolación** y **extrapolación**.

Supongamos que tenemos datos correspondientes al intervalo

$$
x_{\min}\leq x\leq x_{\max}.
$$

Si utilizamos nuestro modelo para estimar un valor correspondiente a

$$
x_{\min}\leq x^\ast\leq x_{\max},
$$

estamos realizando una **interpolación**.

Si, por el contrario,

$$
x^\ast<x_{\min}
$$

o

$$
x^\ast>x_{\max},
$$

estamos realizando una **extrapolación**.

### Interpolación

$$
\boxed{
x^\ast\in[x_{\min},x_{\max}]
}
$$

### Extrapolación

$$
\boxed{
x^\ast\notin[x_{\min},x_{\max}]
}
$$

La diferencia es importante porque dentro del intervalo conocemos cómo se comportan los datos.

Fuera del intervalo debemos suponer que el comportamiento observado continúa.

<br>

### 15.1 Ejemplo

Supongamos que tenemos datos para

$$
1\leq x\leq6.
$$

Una predicción para

$$
x=4
$$

es una interpolación.

Una predicción para

$$
x=8
$$

es una extrapolación.

Aunque matemáticamente podamos evaluar el modelo en ambos puntos, las predicciones no tienen necesariamente el mismo grado de confiabilidad.

Esto es especialmente importante en modelos de regresión.

Por ejemplo, si ajustamos

$$
\hat y=6142.86x+14333.33
$$

a los datos bacterianos del ejemplo anterior, podemos evaluar el modelo en $x=7$.

Pero debemos recordar que los datos originales solo llegan hasta $x=6$.

Por tanto,

$$
\hat y(7)
$$

es una extrapolación.

No sabemos si la población bacteriana continuará aumentando linealmente para concentraciones mayores.

Puede aparecer saturación, competencia, toxicidad u otro mecanismo que haga que el modelo deje de ser válido.

> **Idea fundamental**
>
> Una función puede evaluarse matemáticamente fuera del rango de los datos, pero esto no significa que la predicción sea científicamente válida.

<br>

## 16. ¿Cuándo utilizar regresión y cuándo interpolación?

Una pregunta importante al trabajar con datos es decidir qué estrategia utilizar.

### Utilizamos regresión cuando:

- los datos contienen ruido;
- existen errores de medición;
- buscamos identificar una tendencia;
- queremos estimar parámetros;
- queremos construir un modelo predictivo;
- no esperamos que una función pase exactamente por todos los puntos.

### Utilizamos interpolación cuando:

- los valores conocidos se consideran exactos;
- queremos una función que pase por los datos;
- necesitamos estimar valores entre puntos conocidos;
- conocemos una función únicamente mediante valores tabulados.

Por ejemplo, si medimos experimentalmente la temperatura de un sistema, es razonable esperar errores de medición. En ese caso, una curva que pase exactamente por cada medición podría incluso ser indeseable.

En cambio, si tenemos valores exactos de una función matemática evaluada en determinados puntos, la interpolación puede ser apropiada.

<br><br>

## 17. Ideas principales

Al finalizar este capítulo debemos recordar las siguientes ideas:

1. Los datos pueden utilizarse para construir modelos matemáticos.

2. La regresión lineal permite construir un modelo de la forma

   $$
   \hat y=\hat m x+\hat b.
   $$

3. Los parámetros se determinan mediante el método de mínimos cuadrados.

4. El método minimiza

   $$
   \sum_{i=1}^{n}(y_i-\hat y_i)^2.
   $$

5. Los residuos permiten estudiar la diferencia entre los datos y el modelo.

6. El coeficiente $R^2$ proporciona una medida del ajuste, pero no debe utilizarse como único criterio para validar un modelo.

7. La regresión lineal puede utilizarse como base para construir modelos polinomiales y, mediante transformaciones, modelos exponenciales y de potencias.

8. Un modelo no tiene que ser necesariamente una única función sencilla. En algunos problemas podemos utilizar **modelos por tramos**.

9. La interpolación busca satisfacer exactamente

   $$
   f(x_i)=y_i.
   $$

10. La regresión busca aproximadamente

    $$
    f(x_i)\approx y_i.
    $$

11. La interpolación de Lagrange permite construir un polinomio que pasa exactamente por un conjunto de puntos.

12. La interpolación se utiliza para estimar valores dentro del rango de los datos.

13. La extrapolación utiliza el modelo fuera del rango observado y debe tratarse con especial precaución.

14. La elección de un modelo debe estar guiada por la estructura del fenómeno y por los datos, no únicamente por la facilidad de ajuste.

En resumen,

$$
\boxed{
\text{datos}
\rightarrow
\text{exploración}
\rightarrow
\text{ajuste}
\rightarrow
\text{modelo}
\rightarrow
\text{validación}
\rightarrow
\text{predicción}.
}
$$

<br>

## 18. Ejercicios

### Ejercicio 1. Regresión lineal

Considere los datos

$$
(1,2),\quad
(2,3),\quad
(3,5),\quad
(4,4),\quad
(5,7).
$$

1. Calcule $\bar x$ y $\bar y$.
2. Calcule la pendiente $\hat m$.
3. Calcule el intercepto $\hat b$.
4. Escriba la recta de regresión.
5. Calcule los residuos.
6. Grafique los datos y la recta.
7. Calcule $R^2$.

<br>

### Ejercicio 2. Predicción e interpretación

Suponga que el modelo obtenido para un fenómeno es

$$
\hat y=3.5x+8.
$$

1. ¿Cuál es el valor predicho para $x=4$?
2. Interprete la pendiente.
3. Interprete el intercepto.
4. Si los datos originales corresponden al intervalo $2\leq x\leq8$, determine si la predicción para $x=6$ es una interpolación o una extrapolación.
5. ¿Qué ocurre con una predicción para $x=15$?

<br>

### Ejercicio 3. Modelo exponencial

Considere los datos

| $t$ | $P(t)$ |
|---:|---:|
| 0 | 50 |
| 1 | 74 |
| 2 | 111 |
| 3 | 165 |
| 4 | 247 |

1. Grafique los datos.
2. Proponga un modelo exponencial.
3. Transforme el problema mediante logaritmos.
4. Realice una regresión lineal.
5. Obtenga el modelo exponencial.
6. Compare las predicciones con los datos.

<br>

### Ejercicio 4. Modelo de potencias

Considere los datos

$$
(1,2),\quad
(2,5.8),\quad
(4,17),\quad
(8,49).
$$

Proponga un modelo de la forma

$$
y=Ax^p.
$$

Utilice logaritmos para convertir el problema en una regresión lineal.

<br>

### Ejercicio 5. Interpolación lineal

Considere los puntos

$$
(2,5)
$$

y

$$
(6,13).
$$

1. Construya la función lineal que pasa por ambos puntos.
2. Utilice la función para estimar el valor correspondiente a $x=4$.
3. Explique por qué esta estimación es una interpolación.

<br>

### Ejercicio 6. Interpolación de Lagrange

Considere los puntos

$$
(0,2),\qquad
(1,4),\qquad
(3,5).
$$

1. Construya los polinomios base de Lagrange.
2. Construya el polinomio interpolante.
3. Verifique que el polinomio pasa por los tres puntos.
4. Utilícelo para estimar el valor correspondiente a $x=2$.

<br>

### Ejercicio 7. Regresión o interpolación

Para cada situación determine si sería más apropiado utilizar regresión o interpolación y explique por qué.

1. Se han medido experimentalmente veinte temperaturas y cada medición tiene un error.
2. Se conocen exactamente los valores de una función matemática en diez puntos.
3. Se quiere identificar una tendencia entre horas de estudio y calificación.
4. Se dispone de una tabla exacta de valores de una función y se necesita calcular valores intermedios.

<br>

### Ejercicio 8. Modelo por tramos

Considere los datos

| $x$ | $y$ |
|---:|---:|
| 0 | 2 |
| 1 | 5 |
| 2 | 8 |
| 3 | 11 |
| 4 | 14 |
| 5 | 15 |
| 6 | 14 |
| 7 | 11 |
| 8 | 8 |
| 9 | 5 |
| 10 | 2 |

1. Grafique los datos.
2. Explique por qué una única recta no es un modelo adecuado.
3. Divida el dominio en dos regiones.
4. Ajuste una recta a cada región.
5. Construya el modelo por tramos.
6. Grafique simultáneamente los datos y los dos modelos.
7. Compare el error de los modelos por tramos con el error de una única regresión lineal.
8. Discuta qué ocurre en el punto donde se unen los dos modelos.

<br>

### Ejercicio 9. Construcción de un modelo

Seleccione un fenómeno de interés en física, química, biología, economía o ciencias sociales.

1. Identifique la variable de respuesta.
2. Identifique una o más variables explicativas.
3. Obtenga un conjunto de datos.
4. Grafique los datos.
5. Proponga una forma funcional.
6. Ajuste los parámetros utilizando Python.
7. Calcule los residuos.
8. Evalúe el ajuste.
9. Determine qué predicciones corresponden a interpolación.
10. Determine qué predicciones corresponden a extrapolación.
11. Discuta las limitaciones del modelo.
