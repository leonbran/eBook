# Modelos de cambio continuo

## Introducción

En el capítulo anterior estudiamos modelos de cambio discreto, en los cuales el estado de un sistema se describe mediante una sucesión

$$
x_0,x_1,x_2,\ldots
$$

y la evolución se determina mediante una regla como

$$
x_{n+1}=f(x_n).
$$

Esta descripción resulta apropiada cuando observamos un fenómeno en instantes separados de tiempo: una población al final de cada año, una concentración cada hora, el saldo de una inversión al final de cada mes o el número de individuos de una especie en cada generación.

Sin embargo, muchos fenómenos naturales evolucionan de manera continua. Una población cambia continuamente, una sustancia se desintegra continuamente, la temperatura de un objeto cambia continuamente y la posición de una partícula varía continuamente en el tiempo.

En estos casos resulta natural representar el estado del sistema mediante una función

$$
x=x(t),
$$

donde $t$ representa el tiempo.

La regla de evolución ya no se expresa mediante una relación entre dos estados consecutivos, sino mediante una relación entre la función y su tasa de cambio:

$$
\frac{dx}{dt}=f(x,t).
$$

Estas ecuaciones se denominan **ecuaciones diferenciales ordinarias** (EDO).

La transición conceptual puede representarse mediante

$$
\boxed{
\text{modelo discreto}
\longrightarrow
\text{tasa de cambio}
\longrightarrow
\text{ecuación diferencial}
\longrightarrow
\text{modelo continuo}
}
$$

En este capítulo construiremos y analizaremos modelos continuos de diferentes fenómenos científicos. Estudiaremos modelos de crecimiento y decaimiento, modelos logísticos, sistemas de interacción entre poblaciones y sistemas de ecuaciones diferenciales. También aprenderemos a analizar estos modelos cualitativamente y a obtener soluciones aproximadas mediante métodos numéricos.

La idea central será nuevamente la modelación matemática:

$$
\boxed{
\text{fenómeno}
\longrightarrow
\text{hipótesis}
\longrightarrow
\text{modelo matemático}
\longrightarrow
\text{análisis}
\longrightarrow
\text{interpretación}
}
$$

La principal diferencia es que ahora la evolución del sistema estará gobernada por una tasa de cambio continua.

## 1. De modelos discretos a continuos

### 1.1 Cambio discreto

En un modelo discreto estudiamos el cambio entre dos instantes consecutivos mediante

$$
x_{n+1}-x_n.
$$

Si los instantes están separados por un intervalo de duración $\Delta t$, podemos considerar la tasa de cambio promedio

$$
\frac{x_{n+1}-x_n}{\Delta t}.
$$

Esta expresión indica cuánto cambia, en promedio, la cantidad $x$ por unidad de tiempo durante el intervalo.

Por ejemplo, si una población pasa de $1000$ a $1200$ individuos durante un año, entonces

$$
\frac{x_{n+1}-x_n}{\Delta t}
=
\frac{1200-1000}{1}
=
200.
$$

La población aumentó, en promedio, en $200$ individuos por año durante ese intervalo.

### 1.2 Tasa de cambio instantánea

La tasa de cambio promedio depende del tamaño del intervalo considerado.

Si queremos conocer la tasa de cambio en un instante particular, debemos reducir progresivamente el intervalo.

Para una función continua $x(t)$, la derivada se define mediante

$$
\frac{dx}{dt}
=
\lim_{\Delta t\to0}
\frac{x(t+\Delta t)-x(t)}{\Delta t}.
$$

La derivada representa entonces la **tasa de cambio instantánea** de la variable $x$ respecto del tiempo.

Esta interpretación es fundamental para el modelamiento.

Por ejemplo:

- $\dfrac{dN}{dt}$ representa la tasa de cambio de una población;
- $\dfrac{dC}{dt}$ representa la tasa de cambio de una concentración;
- $\dfrac{dT}{dt}$ representa la tasa de cambio de una temperatura;
- $\dfrac{dv}{dt}$ representa la aceleración de una partícula.

La derivada permite pasar de una descripción basada en cambios entre dos mediciones a una descripción del comportamiento instantáneo del sistema.

### 1.3 De una ecuación discreta a una ecuación diferencial

Consideremos el modelo discreto

$$
x_{n+1}=x_n+r x_n\Delta t.
$$

Restando $x_n$,

$$
x_{n+1}-x_n=r x_n\Delta t.
$$

Dividiendo entre $\Delta t$,

$$
\frac{x_{n+1}-x_n}{\Delta t}=r x_n.
$$

Si hacemos que $\Delta t$ sea cada vez más pequeño, la diferencia cociente se aproxima a una derivada:

$$
\frac{dx}{dt}=rx.
$$

Hemos obtenido una ecuación diferencial a partir de un modelo de cambio discreto.

Este procedimiento ilustra una conexión fundamental:

$$
\boxed{
\frac{x_{n+1}-x_n}{\Delta t}
\longrightarrow
\frac{dx}{dt}
}
$$

cuando

$$
\Delta t\rightarrow0.
$$

### 1.4 Ejemplo: crecimiento proporcional

Supongamos que una población $N(t)$ aumenta a una tasa proporcional a su tamaño.

En un modelo discreto habíamos utilizado

$$
N_{n+1}-N_n=rN_n.
$$

En el modelo continuo, la hipótesis de crecimiento proporcional se expresa mediante

$$
\frac{dN}{dt}=rN.
$$

La interpretación es directa:

> cuanto mayor es la población, mayor es su tasa de crecimiento.

Si la población es el doble, la tasa de crecimiento también es el doble.

Esta ecuación será uno de los modelos fundamentales de este capítulo.

## 2. Fundamentos matemáticos: ecuaciones diferenciales ordinarias

### 2.1 ¿Qué es una ecuación diferencial?

Una ecuación diferencial es una ecuación que relaciona una función desconocida con una o más de sus derivadas.

Por ejemplo,

$$
\frac{dx}{dt}=3x
$$

es una ecuación diferencial ordinaria porque relaciona la función $x(t)$ con su primera derivada.

Otro ejemplo es

$$
\frac{d^2x}{dt^2}+x=0.
$$

En este caso aparece la segunda derivada.

Una ecuación diferencial ordinaria contiene derivadas respecto de una sola variable independiente. Por ello se denomina **ordinaria**.

En este capítulo nos concentraremos principalmente en ecuaciones de primer orden de la forma

$$
\frac{dx}{dt}=f(t,x).
$$

### 2.2 Orden de una ecuación diferencial

El **orden** de una ecuación diferencial corresponde al orden de la derivada de mayor grado que aparece en ella.

Por ejemplo,

$$
\frac{dx}{dt}=x
$$

es una ecuación de primer orden, mientras que

$$
\frac{d^2x}{dt^2}+4\frac{dx}{dt}+3x=0
$$

es una ecuación de segundo orden.

Los modelos de cambio continuo que estudiaremos inicialmente serán principalmente de primer orden.

### 2.3 Solución de una ecuación diferencial

Una solución de una ecuación diferencial es una función que satisface la ecuación en un intervalo determinado.

Por ejemplo, consideremos

$$
\frac{dx}{dt}=x.
$$

La función

$$
x(t)=e^t
$$

es una solución porque

$$
\frac{dx}{dt}=e^t=x(t).
$$

Pero también lo es

$$
x(t)=2e^t,
$$

pues

$$
\frac{dx}{dt}=2e^t=x(t).
$$

En realidad, la familia

$$
x(t)=Ce^t
$$

es una familia de soluciones, donde $C$ es una constante.

Esto plantea una pregunta importante: ¿cómo seleccionamos una solución particular?

La respuesta nos lleva a los problemas de valor inicial.

## 3. Problemas de valor inicial

### 3.1 Ecuación diferencial y condición inicial

Un modelo continuo normalmente contiene dos componentes:

1. una ecuación que describe la regla de evolución;
2. una condición inicial que especifica el estado del sistema en un instante determinado.

Por ejemplo,

$$
\frac{dx}{dt}=f(t,x),
$$

junto con

$$
x(t_0)=x_0.
$$

Este problema se denomina **problema de valor inicial**.

Podemos representarlo como

$$
\boxed{
\text{ecuación diferencial}
+
\text{condición inicial}
=
\text{problema de valor inicial}
}
$$

La ecuación describe cómo evoluciona el sistema, mientras que la condición inicial determina desde qué estado comienza.

### 3.2 Ejemplo

Consideremos

$$
\frac{dx}{dt}=x,
$$

con

$$
x(0)=2.
$$

Sabemos que la solución general es

$$
x(t)=Ce^t.
$$

Utilizando la condición inicial,

$$
x(0)=Ce^0=C=2.
$$

Por tanto,

$$
\boxed{x(t)=2e^t}.
$$

La condición inicial ha permitido seleccionar una única trayectoria dentro de la familia de soluciones.

### 3.3 Interpretación científica

Supongamos que $x(t)$ representa una población.

La ecuación

$$
\frac{dx}{dt}=f(t,x)
$$

describe la dinámica de crecimiento de la población.

La condición

$$
x(0)=x_0
$$

indica cuál era la población en el instante inicial.

Por tanto, un modelo continuo completo debe especificar tanto la ley dinámica como el estado inicial.

## 4. Método de separación de variables

### 4.1 Ecuaciones separables

Una ecuación diferencial de primer orden

$$
\frac{dx}{dt}=f(t,x)
$$

se denomina **separable** si puede escribirse en la forma

$$
\frac{dx}{dt}=g(t)h(x).
$$

En ese caso podemos reorganizarla como

$$
\frac{1}{h(x)}\,dx=g(t)\,dt.
$$

De esta manera, las variables $x$ y $t$ quedan separadas.

### 4.2 Procedimiento

Para resolver una ecuación separable:

1. escribir la ecuación en forma separable;
2. separar las variables;
3. integrar ambos lados;
4. utilizar la condición inicial, si existe;
5. despejar la función cuando sea posible.

### 4.3 Ejemplo: crecimiento exponencial

Consideremos

$$
\frac{dN}{dt}=rN.
$$

Suponiendo $N>0$, podemos escribir

$$
\frac{1}{N}\,dN=r\,dt.
$$

Integramos:

$$
\int\frac{1}{N}\,dN
=
\int r\,dt.
$$

Obtenemos

$$
\ln N=rt+C.
$$

Exponentiando,

$$
N=Ce^{rt}.
$$

Por tanto, la solución general es

$$
\boxed{N(t)=Ce^{rt}}.
$$

Si además

$$
N(0)=N_0,
$$

entonces

$$
C=N_0,
$$

y obtenemos

$$
\boxed{N(t)=N_0e^{rt}}.
$$

Este resultado será la base del modelo de crecimiento exponencial continuo.

### 4.4 Ejemplo: decaimiento

Supongamos que una sustancia pierde una cantidad proporcional a la cantidad presente:

$$
\frac{dC}{dt}=-kC,
$$

donde $k>0$.

Separando variables,

$$
\frac{1}{C}\,dC=-k\,dt.
$$

Integrando,

$$
\ln C=-kt+C_1.
$$

Por tanto,

$$
C(t)=C_0e^{-kt}.
$$

Si inicialmente

$$
C(0)=100,
$$

y

$$
k=0.2,
$$

entonces

$$
\boxed{C(t)=100e^{-0.2t}}.
$$

La cantidad disminuye continuamente, pero nunca se hace exactamente igual a cero.

## 5. Modelos de crecimiento y decaimiento

### 5.1 Modelo de crecimiento exponencial continuo

Supongamos que la tasa de crecimiento de una población es proporcional a su tamaño:

$$
\frac{dN}{dt}=rN.
$$

La solución es

$$
N(t)=N_0e^{rt}.
$$

Si $r>0$, tenemos crecimiento.

Si $r<0$, tenemos decaimiento.

Si $r=0$, la población permanece constante.

### 5.2 Ejemplo: población

Supongamos una población inicial de

$$
N_0=1000
$$

individuos y una tasa de crecimiento continua de

$$
r=0.05.
$$

El modelo es

$$
N(t)=1000e^{0.05t}.
$$

Después de $10$ unidades de tiempo,

$$
N(10)=1000e^{0.5}\approx1648.72.
$$

El modelo predice aproximadamente $1649$ individuos.

### 5.3 Crecimiento discreto versus continuo

En el capítulo anterior obtuvimos el modelo discreto

$$
N_n=N_0(1+r)^n.
$$

El modelo continuo correspondiente es

$$
N(t)=N_0e^{rt}.
$$

Aunque ambos representan crecimiento exponencial, los parámetros tienen interpretaciones diferentes.

En el modelo discreto, $r$ representa una tasa de crecimiento por periodo.

En el modelo continuo, $r$ representa una tasa de crecimiento instantánea.

Esta distinción es importante cuando se comparan modelos discretos y continuos.

### 5.4 Modelo de decaimiento

Muchos procesos pueden modelarse mediante

$$
\frac{dC}{dt}=-kC,
\qquad k>0.
$$

La solución es

$$
C(t)=C_0e^{-kt}.
$$

Este modelo puede utilizarse como aproximación para procesos como:

- decaimiento radiactivo;
- eliminación de ciertas sustancias;
- pérdida de concentración;
- enfriamiento en determinados regímenes;
- reducción de poblaciones bajo determinadas hipótesis.

### 5.5 Vida media

En un modelo de decaimiento

$$
C(t)=C_0e^{-kt},
$$

la vida media $T_{1/2}$ es el tiempo necesario para que la cantidad se reduzca a la mitad:

$$
C(T_{1/2})=\frac{C_0}{2}.
$$

Por tanto,

$$
C_0e^{-kT_{1/2}}
=
\frac{C_0}{2}.
$$

Dividiendo por $C_0$,

$$
e^{-kT_{1/2}}=\frac12.
$$

Tomando logaritmos,

$$
-kT_{1/2}=-\ln2.
$$

Así,

$$
\boxed{
T_{1/2}=\frac{\ln2}{k}
}.
$$

Este resultado permite conectar directamente un parámetro del modelo con una cantidad observable del fenómeno.

## 6. Modelo logístico continuo

### 6.1 Limitaciones del crecimiento exponencial

El modelo exponencial

$$
\frac{dN}{dt}=rN
$$

supone que la tasa de crecimiento por individuo permanece constante.

Como consecuencia,

$$
N(t)\longrightarrow\infty
$$

cuando $t\to\infty$ si $r>0$.

Esta predicción no suele ser realista para poblaciones que disponen de recursos limitados.

Para incorporar esta restricción introducimos una capacidad de carga $K$.

### 6.2 Construcción del modelo

El modelo logístico continuo se escribe como

$$
\boxed{
\frac{dN}{dt}
=
rN\left(1-\frac{N}{K}\right)
}
$$

donde:

- $N(t)$ es el tamaño de la población;
- $r$ es la tasa de crecimiento;
- $K$ es la capacidad de carga.

Cuando $N$ es pequeño comparado con $K$,

$$
1-\frac{N}{K}\approx1,
$$

y recuperamos aproximadamente el modelo exponencial:

$$
\frac{dN}{dt}\approx rN.
$$

Cuando $N$ se aproxima a $K$,

$$
1-\frac{N}{K}\approx0,
$$

y el crecimiento disminuye.

### 6.3 Equilibrios

Los equilibrios satisfacen

$$
\frac{dN}{dt}=0.
$$

Por tanto,

$$
rN\left(1-\frac{N}{K}\right)=0.
$$

Los puntos de equilibrio son

$$
N_1^*=0
$$

y

$$
N_2^*=K.
$$

Estos representan:

- $N^*=0$: extinción;
- $N^*=K$: equilibrio asociado a la capacidad de carga.

### 6.4 Análisis del signo

Supongamos que

$$
r>0,
\qquad
K>0.
$$

Si

$$
0<N<K,
$$

entonces

$$
\frac{dN}{dt}>0.
$$

La población aumenta.

Si

$$
N>K,
$$

entonces

$$
\frac{dN}{dt}<0.
$$

La población disminuye.

Por tanto, las trayectorias positivas tienden hacia $K$.

Esta conclusión puede obtenerse sin resolver explícitamente la ecuación diferencial.

### 6.5 Solución del modelo logístico

El modelo logístico es separable:

$$
\frac{dN}{dt}
=
rN\left(1-\frac{N}{K}\right).
$$

Podemos escribir

$$
\frac{dN}{N(1-N/K)}
=
r\,dt.
$$

Después de integrar y aplicar la condición inicial $N(0)=N_0$, obtenemos

$$
\boxed{
N(t)=
\frac{K}
{1+
\left(\frac{K-N_0}{N_0}\right)e^{-rt}}
}.
$$

Esta solución permite observar explícitamente cómo la población evoluciona desde $N_0$ hacia $K$.

### 6.6 Ejemplo

Supongamos

$$
N_0=20,
\qquad
r=0.3,
\qquad
K=100.
$$

Entonces

$$
N(t)
=
\frac{100}
{1+4e^{-0.3t}}.
$$

Inicialmente,

$$
N(0)=20.
$$

A medida que $t$ aumenta,

$$
e^{-0.3t}\longrightarrow0,
$$

y por tanto

$$
N(t)\longrightarrow100.
$$

El modelo predice que la población se aproxima a la capacidad de carga.

## 7. Modelos de interacción entre poblaciones

### 7.1 Más de una población

Muchos fenómenos ecológicos no pueden describirse mediante una única población.

Por ejemplo, el crecimiento de una especie puede depender de la presencia de otra.

Si $P(t)$ representa una población de presas y $D(t)$ una población de depredadores, podemos considerar un sistema de ecuaciones diferenciales.

Un modelo clásico es

$$
\frac{dP}{dt}
=
rP-aPD,
$$

$$
\frac{dD}{dt}
=
bPD-dD.
$$

Este modelo se conoce como modelo de **Lotka-Volterra**.

### 7.2 Interpretación de los términos

En la ecuación de las presas,

$$
\frac{dP}{dt}
=
rP-aPD,
$$

el término

$$
rP
$$

representa el crecimiento natural de las presas.

El término

$$
-aPD
$$

representa la pérdida de presas debido a la interacción con los depredadores.

En la ecuación de los depredadores,

$$
\frac{dD}{dt}
=
bPD-dD,
$$

el término

$$
bPD
$$

representa el crecimiento de los depredadores debido a la disponibilidad de presas.

El término

$$
-dD
$$

representa la mortalidad natural de los depredadores.

### 7.3 Una idea fundamental de la modelación

El término de interacción $PD$ aparece en ambas ecuaciones, pero con efectos diferentes:

$$
-aPD
$$

en la ecuación de las presas y

$$
+bPD
$$

en la ecuación de los depredadores.

Esto muestra cómo una misma interacción física o biológica puede producir efectos opuestos sobre diferentes componentes de un sistema.

### 7.4 Ejemplo conceptual

Supongamos que inicialmente hay muchas presas y pocos depredadores.

La gran cantidad de presas favorece el crecimiento de los depredadores. A medida que aumenta la población de depredadores, aumenta también la presión sobre las presas.

La disminución de las presas reduce posteriormente el alimento disponible para los depredadores.

Esto puede producir una dinámica cíclica:

$$
\text{más presas}
\rightarrow
\text{más depredadores}
\rightarrow
\text{menos presas}
\rightarrow
\text{menos depredadores}
\rightarrow
\text{más presas}.
$$

Este ejemplo muestra que las ecuaciones diferenciales pueden representar mecanismos de retroalimentación entre diferentes componentes de un sistema.

## 8. Análisis cualitativo de modelos continuos

Una ecuación diferencial no siempre puede resolverse explícitamente.

Incluso cuando existe una fórmula para la solución, esta puede no ser la mejor herramienta para comprender la dinámica del sistema.

Por esta razón es importante desarrollar métodos de **análisis cualitativo**.

Consideremos una ecuación autónoma

$$
\frac{dx}{dt}=f(x).
$$

Antes de intentar resolverla, podemos estudiar directamente la función $f$.

Las preguntas fundamentales son:

1. ¿Cuáles son los puntos de equilibrio?
2. ¿En qué regiones aumenta $x$?
3. ¿En qué regiones disminuye?
4. ¿Qué equilibrios son estables?
5. ¿Hacia dónde evolucionan las soluciones?
6. ¿Qué ocurre cuando modificamos los parámetros?

### 8.1 Preparación de las ecuaciones

Antes de realizar un análisis cualitativo conviene escribir el modelo en una forma apropiada.

Por ejemplo,

$$
\frac{dx}{dt}=rx\left(1-\frac{x}{K}\right)
$$

puede escribirse como

$$
\frac{dx}{dt}
=
rx-\frac{r}{K}x^2.
$$

Esta forma permite identificar fácilmente los términos de crecimiento y regulación.

También puede ser útil definir

$$
f(x)=rx\left(1-\frac{x}{K}\right),
$$

de manera que la ecuación se escriba como

$$
\frac{dx}{dt}=f(x).
$$

A partir de aquí podemos analizar la función $f$ en lugar de trabajar directamente con la ecuación diferencial.

### 8.2 Puntos críticos

Un punto crítico o equilibrio $x^*$ satisface

$$
f(x^*)=0.
$$

En otras palabras,

$$
\frac{dx}{dt}=0.
$$

Por ejemplo, para el modelo logístico,

$$
f(x)=rx\left(1-\frac{x}{K}\right),
$$

los puntos críticos son

$$
x^*=0
$$

y

$$
x^*=K.
$$

### 8.3 Diagrama de fases en una dimensión

Para una ecuación

$$
\frac{dx}{dt}=f(x),
$$

podemos estudiar el signo de $f(x)$.

Si

$$
f(x)>0,
$$

entonces

$$
\frac{dx}{dt}>0,
$$

por lo que $x(t)$ aumenta.

Si

$$
f(x)<0,
$$

entonces

$$
\frac{dx}{dt}<0,
$$

por lo que $x(t)$ disminuye.

Para el modelo logístico, suponiendo $r>0$ y $K>0$:

$$
\begin{array}{c|ccc}
x & (0,K) & K & (K,\infty)\\
\hline
f(x) & + & 0 & -
\end{array}
$$

Por tanto:

$$
0<x<K
\quad\Longrightarrow\quad
x(t)\text{ aumenta},
$$

mientras que

$$
x>K
\quad\Longrightarrow\quad
x(t)\text{ disminuye}.
$$

Esto permite concluir que $K$ es un equilibrio estable.

### 8.4 Campo de velocidades

Una ecuación diferencial

$$
\frac{dx}{dt}=f(t,x)
$$

asigna una tasa de cambio a cada punto del plano $(t,x)$.

En cada punto podemos representar una pequeña flecha cuya pendiente es

$$
\frac{dx}{dt}=f(t,x).
$$

El conjunto de estas flechas constituye un **campo de velocidades** o **campo direccional**.

El campo permite visualizar la dirección en la que evolucionan las soluciones sin necesidad de resolver explícitamente la ecuación.

### 8.5 Ejemplo

Consideremos

$$
\frac{dx}{dt}=x(1-x).
$$

Los puntos críticos satisfacen

$$
x(1-x)=0,
$$

por lo que

$$
x^*=0,
\qquad
x^*=1.
$$

Si

$$
0<x<1,
$$

entonces

$$
x(1-x)>0,
$$

y las soluciones aumentan.

Si

$$
x>1,
$$

entonces

$$
x(1-x)<0,
$$

y las soluciones disminuyen.

Por tanto, las soluciones positivas tienden hacia

$$
x=1.
$$

Esta conclusión puede obtenerse directamente del campo de velocidades y del análisis de signos.

## 9. Sistemas de ecuaciones diferenciales

### 9.1 Introducción

Cuando un fenómeno depende de varias variables que evolucionan simultáneamente, necesitamos un sistema de ecuaciones diferenciales.

Un sistema de dos variables puede escribirse como

$$
\frac{dx}{dt}=f(x,y),
$$

$$
\frac{dy}{dt}=g(x,y).
$$

De manera compacta,

$$
\boxed{
\frac{d\mathbf{x}}{dt}
=
\mathbf{F}(\mathbf{x})
}
$$

donde

$$
\mathbf{x}(t)
=
\begin{pmatrix}
x(t)\\
y(t)
\end{pmatrix}.
$$

### 9.2 Ejemplo: modelo presa-depredador

El modelo de Lotka-Volterra puede escribirse como

$$
\frac{dP}{dt}
=
rP-aPD,
$$

$$
\frac{dD}{dt}
=
bPD-dD.
$$

En forma vectorial,

$$
\frac{d}{dt}
\begin{pmatrix}
P\\
D
\end{pmatrix}
=
\begin{pmatrix}
rP-aPD\\
bPD-dD
\end{pmatrix}.
$$

Esta representación será especialmente útil cuando implementemos el modelo computacionalmente.

### 9.3 Puntos críticos de un sistema

Un punto crítico $(x^*,y^*)$ satisface simultáneamente

$$
f(x^*,y^*)=0
$$

y

$$
g(x^*,y^*)=0.
$$

Es decir,

$$
\frac{dx}{dt}=0,
\qquad
\frac{dy}{dt}=0.
$$

Para el modelo presa-depredador,

$$
rP-aPD=0,
$$

$$
bPD-dD=0.
$$

Factorizando,

$$
P(r-aD)=0,
$$

$$
D(bP-d)=0.
$$

Los puntos críticos son

$$
(P^*,D^*)=(0,0)
$$

y

$$
(P^*,D^*)
=
\left(
\frac{d}{b},
\frac{r}{a}
\right).
$$

Estos representan estados en los cuales ambas poblaciones permanecen constantes.

### 9.4 Plano de fases

En sistemas de dos variables podemos representar las trayectorias en el plano $(x,y)$.

Una solución

$$
x=x(t),
\qquad
y=y(t)
$$

genera una curva

$$
(x(t),y(t))
$$

en el plano.

Esta representación se denomina **plano de fases**.

El plano de fases permite estudiar:

- puntos de equilibrio;
- trayectorias;
- ciclos;
- estabilidad;
- atracción;
- separación entre diferentes comportamientos.

El análisis cualitativo de sistemas de ecuaciones diferenciales constituye una herramienta fundamental para estudiar modelos cuya solución explícita puede ser difícil o imposible de obtener.

## 10. Técnicas numéricas para analizar modelos continuos

En muchos modelos científicos no podemos encontrar una solución explícita.

Por ejemplo, una ecuación como

$$
\frac{dx}{dt}=f(t,x)
$$

puede no tener una solución expresable mediante funciones elementales.

En estos casos podemos aproximar la solución mediante métodos numéricos.

La idea general consiste en reemplazar la evolución continua por una secuencia de aproximaciones:

$$
x(t_0),x(t_1),x(t_2),\ldots
$$

donde

$$
t_{n+1}=t_n+h
$$

y $h$ es el tamaño del paso.

La estructura general puede representarse como

$$
\boxed{
\text{ecuación diferencial}
\rightarrow
\text{discretización}
\rightarrow
\text{algoritmo}
\rightarrow
\text{aproximación numérica}
}
$$

### 10.1 Método de Euler

Consideremos el problema de valor inicial

$$
\frac{dx}{dt}=f(t,x),
\qquad
x(t_0)=x_0.
$$

La derivada puede aproximarse mediante

$$
\frac{x(t+h)-x(t)}{h}
\approx
\frac{dx}{dt}.
$$

Por tanto,

$$
x(t+h)
\approx
x(t)+hf(t,x(t)).
$$

Definimos las aproximaciones

$$
x_n\approx x(t_n),
$$

con

$$
t_n=t_0+nh.
$$

Obtenemos entonces el método de Euler:

$$
\boxed{
x_{n+1}
=
x_n+h f(t_n,x_n)
}
$$

### 10.2 Interpretación geométrica

El método de Euler utiliza la pendiente de la solución en el punto actual para aproximar la solución durante el siguiente intervalo.

Si

$$
\frac{dx}{dt}=f(t,x),
$$

la pendiente en $(t_n,x_n)$ es

$$
f(t_n,x_n).
$$

Por tanto, Euler avanza aproximadamente siguiendo la recta tangente:

$$
x_{n+1}
=
x_n+h f(t_n,x_n).
$$

El método reemplaza la curva real por una sucesión de pequeños segmentos lineales.

### 10.3 Ejemplo

Consideremos

$$
\frac{dx}{dt}=x,
\qquad
x(0)=1.
$$

La solución exacta es

$$
x(t)=e^t.
$$

Tomemos

$$
h=0.1.
$$

El método de Euler produce

$$
x_{n+1}=x_n+0.1x_n
=
1.1x_n.
$$

Comenzando con

$$
x_0=1,
$$

obtenemos

$$
x_1=1.1,
$$

$$
x_2=1.21,
$$

$$
x_3=1.331.
$$

En general,

$$
x_n=(1.1)^n.
$$

Aunque la solución exacta es

$$
e^{0.1n},
$$

el método de Euler proporciona una aproximación basada únicamente en operaciones elementales.

### 10.4 Implementación en Python

```python
import numpy as np
import matplotlib.pyplot as plt

def f(t, x):
    return x

x0 = 1.0
t0 = 0.0
tf = 2.0
h = 0.1

t = np.arange(t0, tf + h, h)
x = np.zeros(len(t))

x[0] = x0

for n in range(len(t) - 1):
    x[n + 1] = x[n] + h * f(t[n], x[n])

x_exact = np.exp(t)

plt.plot(t, x, label="Euler")
plt.plot(t, x_exact, label="Solución exacta")
plt.xlabel("t")
plt.ylabel("x(t)")
plt.legend()
plt.grid()
plt.show()
```

La comparación entre la solución exacta y la aproximación permite estudiar el error numérico.

## 11. Método de Adams

### 11.1 Idea general

El método de Euler utiliza únicamente la información disponible en el punto actual.

Los métodos de Adams pertenecen a una familia de métodos de **pasos múltiples**. En lugar de utilizar solamente el valor actual, utilizan información obtenida en varios pasos anteriores.

Para

$$
\frac{dx}{dt}=f(t,x),
$$

una aproximación sencilla de Adams-Bashforth de dos pasos es

$$
\boxed{
x_{n+1}
=
x_n+
\frac{h}{2}
\left[
3f(t_n,x_n)
-
f(t_{n-1},x_{n-1})
\right]
}
$$

Este método utiliza las pendientes de los dos últimos puntos para extrapolar la solución.

### 11.2 Comparación con Euler

Euler utiliza

$$
x_{n+1}
=
x_n+h f(t_n,x_n).
$$

Adams-Bashforth de dos pasos utiliza

$$
x_{n+1}
=
x_n+
\frac{h}{2}
\left[
3f_n-f_{n-1}
\right].
$$

La ventaja es que el método puede obtener mayor precisión para un mismo tamaño de paso.

Sin embargo, aparece una nueva dificultad: necesitamos conocer más de un valor inicial.

Para iniciar un método de dos pasos, por ejemplo, necesitamos conocer $x_0$ y $x_1$. El valor $x_1$ puede obtenerse mediante Euler u otro método de un paso.

### 11.3 Ejemplo conceptual

Supongamos que conocemos

$$
x_{n-1},
\qquad
x_n,
$$

y las pendientes correspondientes

$$
f_{n-1}=f(t_{n-1},x_{n-1}),
$$

$$
f_n=f(t_n,x_n).
$$

Adams-Bashforth utiliza esta información para estimar la pendiente futura y construir una aproximación más precisa de $x_{n+1}$.

Esta idea conduce a una familia amplia de métodos de pasos múltiples.

## 12. Discusión sobre métodos de orden superior

### 12.1 Precisión de un método numérico

Una cuestión fundamental en los métodos numéricos es determinar qué tan rápido disminuye el error cuando reducimos el tamaño de paso $h$.

Un método de orden $p$ tiene, en términos generales, un error global que se comporta como

$$
E(h)=O(h^p).
$$

Por ejemplo, un método de primer orden tiene

$$
E(h)=O(h),
$$

mientras que un método de cuarto orden tiene

$$
E(h)=O(h^4).
$$

Esto significa que reducir el tamaño del paso puede producir una disminución mucho más rápida del error en un método de orden superior.

### 12.2 Método de Runge-Kutta de cuarto orden

Uno de los métodos más conocidos es el método de Runge-Kutta de cuarto orden, denominado RK4.

Para

$$
\frac{dx}{dt}=f(t,x),
$$

se calculan

$$
k_1=f(t_n,x_n),
$$

$$
k_2=f\left(t_n+\frac{h}{2},
x_n+\frac{h}{2}k_1\right),
$$

$$
k_3=f\left(t_n+\frac{h}{2},
x_n+\frac{h}{2}k_2\right),
$$

$$
k_4=f(t_n+h,x_n+hk_3).
$$

Finalmente,

$$
\boxed{
x_{n+1}
=
x_n+
\frac{h}{6}
(k_1+2k_2+2k_3+k_4)
}
$$

El método utiliza varias evaluaciones de la función $f$ dentro de cada paso para obtener una aproximación más precisa.

### 12.3 ¿Por qué utilizar métodos de orden superior?

Euler es sencillo y fácil de implementar, pero puede requerir pasos muy pequeños para obtener una buena precisión.

Los métodos de orden superior permiten alcanzar una precisión comparable utilizando pasos más grandes.

Sin embargo, mayor orden no significa automáticamente que un método sea mejor en todas las situaciones.

También debemos considerar:

- costo computacional;
- estabilidad;
- tamaño de paso;
- acumulación de errores;
- propiedades del modelo;
- rigidez del sistema.

Por tanto, elegir un método numérico es parte del proceso de modelación computacional.

### 12.4 Ejemplo comparativo

Consideremos nuevamente

$$
\frac{dx}{dt}=x,
\qquad
x(0)=1.
$$

La solución exacta es

$$
x(t)=e^t.
$$

Podemos resolver el problema utilizando Euler, Adams-Bashforth o RK4 y comparar las aproximaciones.

Una estrategia experimental consiste en repetir la simulación con

$$
h=0.1,\qquad
h=0.05,\qquad
h=0.025
$$

y estudiar cómo disminuye el error.

Esta comparación permite observar experimentalmente la relación entre el tamaño del paso y el orden del método.

## 13. Ejercicios

### Ejercicio 1. De discreto a continuo

Considere el modelo discreto

$$
N_{n+1}=N_n+rN_n\Delta t.
$$

1. Reorganice la ecuación para obtener una expresión para la diferencia cociente.
2. Explique qué ocurre cuando $\Delta t\to0$.
3. Obtenga la ecuación diferencial correspondiente.
4. Resuelva el modelo continuo.
5. Compare la solución discreta y continua.

### Ejercicio 2. Crecimiento exponencial

Una población tiene inicialmente $2000$ individuos y crece a una tasa continua del $4\%$.

1. Construya el modelo diferencial.
2. Formule el problema de valor inicial.
3. Resuelva la ecuación mediante separación de variables.
4. Determine la población después de $10$ años.
5. Determine cuándo la población alcanzará $5000$ individuos.

### Ejercicio 3. Decaimiento

Una sustancia satisface

$$
\frac{dC}{dt}=-0.15C,
$$

con

$$
C(0)=100.
$$

1. Resuelva la ecuación.
2. Determine la concentración después de $10$ unidades de tiempo.
3. Calcule la vida media.
4. ¿Cuánto tiempo debe transcurrir para que la concentración sea menor que $10$?

### Ejercicio 4. Modelo logístico

Considere

$$
\frac{dN}{dt}
=
0.2N
\left(1-\frac{N}{500}\right),
$$

con

$$
N(0)=20.
$$

1. Determine los puntos de equilibrio.
2. Analice su estabilidad mediante el signo de $dN/dt$.
3. Resuelva la ecuación diferencial.
4. Determine el valor límite de $N(t)$ cuando $t\to\infty$.
5. Grafique la solución.
6. Compare la solución con el modelo exponencial correspondiente.

### Ejercicio 5. Campo de velocidades

Considere

$$
\frac{dx}{dt}=x(1-x).
$$

1. Determine los puntos críticos.
2. Determine el signo de $dx/dt$ en los intervalos determinados por los puntos críticos.
3. Determine cuáles equilibrios son estables.
4. Dibuje un diagrama de fase.
5. Describa cualitativamente el comportamiento de las soluciones para diferentes condiciones iniciales.

### Ejercicio 6. Problema de valor inicial

Considere

$$
\frac{dx}{dt}=2x+3,
$$

con

$$
x(0)=1.
$$

1. Determine la solución exacta.
2. Calcule $x(1)$.
3. Utilice el método de Euler con $h=0.1$ para aproximar $x(1)$.
4. Compare el resultado numérico con la solución exacta.
5. Repita el cálculo utilizando $h=0.05$.
6. Analice cómo cambia el error.

### Ejercicio 7. Método de Euler

Considere

$$
\frac{dx}{dt}=x(1-x),
\qquad
x(0)=0.1.
$$

1. Implemente el método de Euler.
2. Utilice $h=0.1$.
3. Simule hasta $t=20$.
4. Grafique la solución aproximada.
5. Compare el resultado con la solución exacta del modelo logístico.
6. Repita utilizando $h=0.05$.

### Ejercicio 8. Comparación de métodos

Considere

$$
\frac{dx}{dt}=x,
\qquad
x(0)=1.
$$

Implemente:

- Euler;
- Adams-Bashforth de dos pasos;
- RK4.

Utilice diferentes tamaños de paso y compare las soluciones con

$$
x(t)=e^t.
$$

Analice:

1. el error;
2. el costo computacional;
3. la influencia del tamaño de paso;
4. la precisión de cada método.

### Ejercicio 9. Sistema presa-depredador

Considere

$$
\frac{dP}{dt}=0.1P-0.01PD,
$$

$$
\frac{dD}{dt}=0.005PD-0.1D.
$$

con

$$
P(0)=40,
\qquad
D(0)=10.
$$

1. Determine los puntos críticos.
2. Interprete cada punto crítico.
3. Implemente el sistema utilizando un método numérico.
4. Grafique las poblaciones en función del tiempo.
5. Grafique la trayectoria en el plano $(P,D)$.
6. Describa el comportamiento observado.

### Ejercicio 10. Construcción de un modelo continuo

Seleccione un fenómeno científico en alguna de las siguientes áreas:

- biología;
- ecología;
- química;
- física;
- ciencias ambientales;
- economía.

Construya un modelo continuo siguiendo las etapas:

1. describa el fenómeno;
2. identifique las variables;
3. establezca las hipótesis;
4. defina los parámetros;
5. determine una ley de tasa de cambio;
6. construya la ecuación diferencial;
7. especifique la condición inicial;
8. analice los puntos de equilibrio;
9. estudie cualitativamente el modelo;
10. encuentre una solución analítica si es posible;
11. implemente una solución numérica;
12. grafique los resultados;
13. interprete el comportamiento;
14. discuta las limitaciones del modelo.

El objetivo no es únicamente resolver una ecuación diferencial, sino mostrar cómo una hipótesis sobre un fenómeno conduce a una ley de cambio y cómo dicha ley permite realizar predicciones.

## 14. Hacia modelos más complejos

En este capítulo hemos pasado de modelos discretos

$$
x_{n+1}=f(x_n)
$$

a modelos continuos de la forma

$$
\frac{dx}{dt}=f(t,x).
$$

Hemos visto que las ecuaciones diferenciales permiten representar tasas de cambio y que los problemas de valor inicial incorporan las condiciones particulares del sistema.

También hemos estudiado modelos de crecimiento y decaimiento, regulación poblacional, interacción entre especies y sistemas de ecuaciones diferenciales.

Una idea especialmente importante es que existen diferentes niveles de análisis.

Podemos comenzar con una ecuación diferencial:

$$
\frac{dx}{dt}=f(x),
$$

y estudiar sus puntos de equilibrio y el signo de $f(x)$ sin encontrar explícitamente una solución.

También podemos buscar una solución analítica mediante técnicas como la separación de variables.

Finalmente, cuando una solución explícita no está disponible o resulta difícil de obtener, podemos utilizar métodos numéricos:

$$
\boxed{
\text{modelo}
\rightarrow
\text{ecuación diferencial}
\rightarrow
\text{análisis cualitativo}
\rightarrow
\text{solución analítica o numérica}
}
$$

En modelos con muchas variables, esta estructura conduce naturalmente al estudio de sistemas dinámicos, análisis de estabilidad, métodos numéricos para sistemas de ecuaciones y, posteriormente, a modelos más sofisticados como ecuaciones diferenciales parciales.

Los modelos continuos constituyen así un punto de encuentro entre el cálculo, las ecuaciones diferenciales, el análisis cualitativo, la computación científica y el modelamiento matemático.
