# Modelos de Markov

Los modelos probabilísticos son representaciones matemáticas utilizadas para describir y analizar fenómenos o sistemas que presentan incertidumbre o variabilidad. A diferencia de los modelos deterministas, en los que las condiciones iniciales y los parámetros determinan completamente la evolución del sistema, los modelos probabilísticos incorporan explícitamente el azar.

Estos modelos se fundamentan en la teoría de la probabilidad y permiten cuantificar la incertidumbre asociada con diferentes resultados posibles. Se utilizan ampliamente en estadística, ciencias de la computación, ingeniería, economía, ciencias sociales, física, biología y muchas otras disciplinas.

Una característica fundamental de los modelos estocásticos es que, aun cuando las condiciones iniciales y las reglas de evolución sean conocidas, el resultado de una realización particular no necesariamente puede predecirse con certeza. En consecuencia, en lugar de estudiar una única trayectoria determinada, resulta necesario estudiar probabilidades, distribuciones y conjuntos de posibles trayectorias.

En este capítulo introduciremos algunos conceptos básicos de probabilidad y variables aleatorias para, posteriormente, construir modelos estocásticos mediante **cadenas de Markov**. Prestaremos especial atención a la matriz de transición, la evolución de las distribuciones de probabilidad, las trayectorias de una cadena, su verosimilitud y su comportamiento a largo plazo.

Finalmente, introduciremos las **cadenas de Markov ocultas**, en las cuales el estado del sistema no puede observarse directamente y únicamente tenemos acceso a observaciones relacionadas probabilísticamente con dichos estados.

<br><br>

## 1. Fundamentos matemáticos: cálculo de probabilidades

La teoría de la probabilidad proporciona un lenguaje matemático para describir fenómenos aleatorios. Para construir este lenguaje necesitamos especificar cuáles son los posibles resultados de un experimento y cómo se asignan probabilidades a los eventos que pueden ocurrir.

<br><br>

### 1.1 Espacio muestral

Un **espacio muestral** es el conjunto de todos los resultados posibles de un experimento aleatorio. Se denota generalmente por $\Omega$.

Por ejemplo, si lanzamos una moneda, podemos considerar

$$
\Omega = \{\text{Cara},\text{Cruz}\}.
$$

Si lanzamos un dado de seis caras,

$$
\Omega = \{1,2,3,4,5,6\}.
$$

Si lanzamos dos dados y distinguimos el resultado de cada dado, podemos escribir

$$
\Omega =
\{(1,1),(1,2),\ldots,(6,5),(6,6)\}.
$$

El espacio muestral puede ser finito, infinito numerable o incluso no numerable.

<br><br>

### 1.2 Eventos

Un **evento** es un subconjunto del espacio muestral. Por ejemplo, al lanzar un dado, podemos definir

$$
A=\{2,4,6\},
$$

donde $A$ representa el evento "obtener un número par".

Los eventos pueden combinarse mediante las operaciones usuales de conjuntos:

* $A\cup B$: ocurre $A$ o $B$.
* $A\cap B$: ocurren simultáneamente $A$ y $B$.
* $A^c$: no ocurre $A$.
* $A\setminus B$: ocurre $A$ pero no $B$.

<br><br>

### 1.3 Probabilidad

Una probabilidad es una función que asigna a cada evento $A$ un número entre $0$ y $1$:

$$
P:\mathcal{F}\longrightarrow [0,1],
$$

donde $\mathcal{F}$ representa la colección de eventos a los que se les puede asignar probabilidad.

La función $P$ satisface los siguientes axiomas.

**No negatividad**

$$
P(A)\geq 0.
$$

**Normalización**

$$
P(\Omega)=1.
$$

**Aditividad**

Si $A_1,A_2,\ldots$ son eventos mutuamente excluyentes, entonces

$$
P\left(\bigcup_{i=1}^{\infty}A_i\right)
=
\sum_{i=1}^{\infty}P(A_i).
$$

Estos axiomas constituyen la base matemática de la teoría de la probabilidad.

<br><br>

### 1.4 Algunas reglas básicas de probabilidad

Si $A$ y $B$ son eventos, entonces

$$
P(A\cup B)
=
P(A)+P(B)-P(A\cap B).
$$

Si $A$ y $B$ son mutuamente excluyentes,

$$
P(A\cap B)=0,
$$

y por tanto

$$
P(A\cup B)=P(A)+P(B).
$$

La probabilidad del evento complementario es

$$
P(A^c)=1-P(A).
$$

<br><br>

### 1.5 Probabilidad condicional

La probabilidad de que ocurra $A$ sabiendo que ha ocurrido $B$ se define como

$$
P(A\mid B)
=
\frac{P(A\cap B)}{P(B)},
\qquad P(B)>0.
$$

Esta definición permite describir situaciones en las que la información disponible modifica las probabilidades.

De manera equivalente,

$$
P(A\cap B)
=
P(A\mid B)P(B).
$$

Esta expresión será especialmente importante al estudiar las trayectorias de las cadenas de Markov.

<br><br>

### 1.6 Independencia

Dos eventos $A$ y $B$ son independientes si la ocurrencia de uno no modifica la probabilidad del otro. Matemáticamente,

$$
P(A\cap B)=P(A)P(B).
$$

Equivalentemente, cuando $P(B)>0$,

$$
P(A\mid B)=P(A).
$$

Es importante distinguir entre **eventos mutuamente excluyentes** e **independientes**. Si dos eventos tienen probabilidad positiva y son mutuamente excluyentes, no pueden ser independientes.

<br><br>

### 1.7 Ejemplo: lanzamiento de un dado

Consideremos un dado justo.

Definimos

$$
A=\{2,4,6\},
$$

como el evento de obtener un número par, y

$$
B=\{4,5,6\},
$$

como el evento de obtener un número mayor o igual que $4$.

Entonces

$$
P(A)=\frac{3}{6}=\frac12,
$$

y

$$
P(B)=\frac{3}{6}=\frac12.
$$

Además,

$$
A\cap B=\{4,6\},
$$

por lo que

$$
P(A\cap B)=\frac{2}{6}=\frac13.
$$

Así,

$$
P(A\cup B)
=
\frac12+\frac12-\frac13
=
\frac23.
$$

<br><br>

## 2. Variables aleatorias

Una variable aleatoria permite transformar los resultados de un experimento aleatorio en cantidades numéricas que pueden ser analizadas matemáticamente.

Formalmente, una variable aleatoria es una función

$$
X:\Omega\longrightarrow \mathbb{R}.
$$

A cada resultado $\omega\in\Omega$ le corresponde un número $X(\omega)$.

Por ejemplo, si lanzamos una moneda tres veces, podemos definir

$$
X=\text{número de caras obtenidas}.
$$

El espacio muestral es

$$
\Omega=
\{CCC,CCS,CSC,CSS,SCC,SCS,SSC,SSS\}.
$$

La variable $X$ toma valores

$$
X\in\{0,1,2,3\}.
$$

<br><br>

### 2.1 Variables aleatorias discretas y continuas

Una variable aleatoria es **discreta** cuando sus posibles valores forman un conjunto finito o numerable.

Por ejemplo, el número de caras obtenidas al lanzar una moneda varias veces es una variable aleatoria discreta.

Una variable aleatoria es **continua** cuando puede tomar valores en un conjunto no numerable, generalmente un intervalo de $\mathbb{R}$.

Por ejemplo, el tiempo de espera de una persona para ser atendida puede modelarse mediante una variable aleatoria continua.

<br><br>

### 2.2 Función de masa de probabilidad

Si $X$ es una variable aleatoria discreta, su función de masa de probabilidad está dada por

$$
p_X(x)=P(X=x).
$$

Debe satisfacer

$$
p_X(x)\geq 0
$$

y

$$
\sum_x p_X(x)=1.
$$

La probabilidad de que $X$ pertenezca a un conjunto $A$ se obtiene mediante

$$
P(X\in A)
=
\sum_{x\in A}p_X(x).
$$

<br><br>

### 2.3 Ejemplo: número de caras

Supongamos que lanzamos una moneda justa tres veces y definimos $X$ como el número de caras.

Los posibles valores son

$$
X\in\{0,1,2,3\}.
$$

Las probabilidades son

$$
P(X=0)=\frac18,
$$

$$
P(X=1)=\frac38,
$$

$$
P(X=2)=\frac38,
$$

y

$$
P(X=3)=\frac18.
$$

Por ejemplo,

$$
P(1\leq X\leq 2)
=
P(X=1)+P(X=2)
=
\frac38+\frac38
=
\frac34.
$$

<br><br>

### 2.4 Esperanza y varianza

Para una variable aleatoria discreta, su esperanza matemática se define como

$$
E[X]
=
\sum_x xP(X=x).
$$

La esperanza representa, en cierto sentido, el valor promedio que se obtendría al repetir muchas veces el experimento.

La varianza se define mediante

$$
\operatorname{Var}(X)
=
E[(X-E[X])^2].
$$

Estas cantidades serán útiles posteriormente para caracterizar el comportamiento de variables y procesos aleatorios.

<br><br>

### 2.5 Ejemplo: selección de individuos

Supongamos que una población contiene $50$ individuos, de los cuales $20$ presentan una determinada característica genética. Se seleccionan $10$ individuos **sin reposición** y definimos

$$
X=\text{número de individuos seleccionados que presentan la característica}.
$$

En este caso, $X$ no sigue una distribución binomial, porque las selecciones no son independientes. El modelo apropiado es la distribución hipergeométrica:

$$
P(X=k)
=
\frac{\binom{20}{k}\binom{30}{10-k}}
{\binom{50}{10}}.
$$

Por ejemplo, la probabilidad de que entre los 10 individuos seleccionados haya entre 3 y 5 individuos con la característica es

$$
P(3\leq X\leq5)
=
\sum_{k=3}^{5}
\frac{\binom{20}{k}\binom{30}{10-k}}
{\binom{50}{10}}.
$$

Este ejemplo muestra que la elección del modelo probabilístico depende de las características del experimento.

<br><br>

## 3. Procesos estocásticos

Una variable aleatoria describe el resultado de un experimento aleatorio. En muchas aplicaciones, sin embargo, estamos interesados en sistemas que evolucionan en el tiempo.

Para representar estos sistemas introducimos los **procesos estocásticos**.

Un proceso estocástico es una familia de variables aleatorias

$$
\{X_t\}_{t\in T},
$$

donde $T$ representa el conjunto de tiempos o índices.

Cuando

$$
T=\{0,1,2,\ldots\},
$$

tenemos un proceso en tiempo discreto.

Cuando

$$
T=[0,\infty),
$$

tenemos un proceso en tiempo continuo.

<br><br>

### 3.1 Trayectoria de un proceso estocástico

Una realización particular de un proceso estocástico puede escribirse como

$$
x_0,x_1,x_2,\ldots
$$

y recibe el nombre de **trayectoria** o realización del proceso.

Es importante distinguir entre el proceso aleatorio y una trayectoria particular.

El proceso $X_t$ describe todas las posibilidades probabilísticas del sistema, mientras que una trayectoria

$$
X_0=x_0,\quad X_1=x_1,\quad X_2=x_2,\ldots
$$

representa una realización concreta.

<br><br>

### 3.2 Ejemplo

Supongamos que $X_t$ representa el estado del clima durante el día $t$, con tres posibles estados:

$$
S=\text{soleado},
\qquad
N=\text{nublado},
\qquad
L=\text{lluvioso}.
$$

Una posible trayectoria podría ser

$$
S,S,N,L,L,N,S,\ldots
$$

Otra realización del mismo proceso podría ser

$$
L,N,N,S,S,S,N,\ldots
$$

El modelo probabilístico determina qué tan probable es cada una de estas trayectorias.

<br><br>

## 4. Cadenas de Markov en tiempo discreto

Las cadenas de Markov constituyen una clase particularmente importante de procesos estocásticos.

La idea central es que, para predecir el estado futuro, basta conocer el estado presente. La información adicional contenida en la trayectoria pasada no modifica la distribución del siguiente estado.

Esta propiedad se conoce como **propiedad de Markov** o propiedad de ausencia de memoria.

<br><br>

### 4.1 Propiedad de Markov

Sea

$$
X_0,X_1,X_2,\ldots
$$

un proceso estocástico en tiempo discreto.

Diremos que satisface la propiedad de Markov si

$$
P(X_{t+1}=x_{t+1}
\mid
X_t=x_t,X_{t-1}=x_{t-1},\ldots,X_0=x_0)
$$

es igual a

$$
P(X_{t+1}=x_{t+1}\mid X_t=x_t).
$$

En otras palabras,

$$
\boxed{
P(X_{t+1}=x_{t+1}\mid X_t=x_t,\ldots,X_0=x_0)
=
P(X_{t+1}=x_{t+1}\mid X_t=x_t)
}
$$

La historia completa del sistema puede ser reemplazada, para predecir el siguiente estado, por el conocimiento del estado actual.

<br><br>

### 4.2 Cadenas homogéneas

Una cadena de Markov es **homogénea** si las probabilidades de transición no dependen del tiempo.

En este caso,

$$
P(X_{t+1}=j\mid X_t=i)=P_{ij}
$$

para todo $t$.

La matriz

$$
P=(P_{ij})
$$

se denomina **matriz de transición**.

<br><br>

### 4.3 Matriz de transición

Si existen $n$ estados posibles, la matriz de transición es

$$
P=
\begin{pmatrix}
P_{11} & P_{12} & \cdots & P_{1n}\\
P_{21} & P_{22} & \cdots & P_{2n}\\
\vdots & \vdots & \ddots & \vdots\\
P_{n1} & P_{n2} & \cdots & P_{nn}
\end{pmatrix},
$$

donde

$$
P_{ij}=P(X_{t+1}=j\mid X_t=i).
$$

Cada entrada satisface

$$
P_{ij}\geq0
$$

y cada fila debe sumar uno:

$$
\sum_{j=1}^{n}P_{ij}=1.
$$

Por esta razón, $P$ se denomina una **matriz estocástica**.

<br><br>

## 5. Evolución de la distribución de estados

Supongamos que la cadena tiene $n$ estados y definimos el vector fila

$$
\mathbf{v}_t
=
(P(X_t=1),\ldots,P(X_t=n)).
$$

Entonces

$$
\mathbf{v}_{t+1}
=
\mathbf{v}_tP.
$$

Iterando,

$$
\mathbf{v}_2
=
\mathbf{v}_0P^2,
$$

y, en general,

$$
\boxed{
\mathbf{v}_t=\mathbf{v}_0P^t
}.
$$

Esta expresión constituye una de las herramientas fundamentales para analizar cadenas de Markov.

<br><br>

### 5.1 Ejemplo: modelo climático

Consideremos los estados

$$
S=\text{soleado},\qquad
N=\text{nublado},\qquad
L=\text{lluvioso}.
$$

Supongamos que

$$
P=
\begin{pmatrix}
0.7&0.2&0.1\\
0.3&0.4&0.3\\
0.2&0.3&0.5
\end{pmatrix}.
$$

Si inicialmente el día es soleado con probabilidad uno,

$$
\mathbf{v}_0=(1,0,0).
$$

Entonces

$$
\mathbf{v}_1
=
\mathbf{v}_0P
=
(0.7,0.2,0.1).
$$

Después de dos días,

$$
\mathbf{v}_2
=
\mathbf{v}_1P
=
(0.57,0.25,0.18).
$$

Por tanto, después de dos pasos, las probabilidades de que el sistema se encuentre en los estados $S$, $N$ y $L$ son, respectivamente,

$$
57\%,\qquad25\%,\qquad18\%.
$$

<br><br>

### 5.2 Probabilidades de transición en varios pasos

La entrada $(i,j)$ de la matriz $P^n$ tiene una interpretación probabilística:

$$
\boxed{
(P^n)_{ij}
=
P(X_{t+n}=j\mid X_t=i)
}.
$$

Por ejemplo, $(P^2)_{ij}$ representa la probabilidad de pasar del estado $i$ al estado $j$ después de dos pasos, independientemente del estado intermedio.

<br><br>

## 6. Trayectorias de una cadena de Markov

Una trayectoria de longitud $n$ de una cadena de Markov es una secuencia

$$
x_0,x_1,\ldots,x_n.
$$

La probabilidad de observar exactamente esta trayectoria es

$$
P(X_0=x_0,X_1=x_1,\ldots,X_n=x_n).
$$

Utilizando la regla de la probabilidad condicional,

$$
\begin{aligned}
&P(X_0=x_0,X_1=x_1,\ldots,X_n=x_n)\\
&=
P(X_0=x_0)
P(X_1=x_1\mid X_0=x_0)
\cdots\\
&\qquad\qquad
P(X_n=x_n\mid X_{n-1}=x_{n-1},\ldots,X_0=x_0).
\end{aligned}
$$

La propiedad de Markov permite simplificar esta expresión:

$$
\boxed{
P(X_0=x_0,\ldots,X_n=x_n)
=
\pi_{x_0}
\prod_{t=1}^{n}P_{x_{t-1}x_t}
}
$$

donde

$$
\pi_{x_0}=P(X_0=x_0)
$$

es la probabilidad inicial.

<br><br>

### 6.1 Ejemplo de una trayectoria

Consideremos una cadena con estados $A$, $M$ y $E$ y matriz de transición

$$
P=
\begin{pmatrix}
0.50&0.30&0.20\\
0.40&0.50&0.10\\
0.30&0.40&0.30
\end{pmatrix}.
$$

Supongamos que la distribución inicial es

$$
\boldsymbol{\pi}=(0,0,1),
$$

por lo que inicialmente estamos en el estado $E$.

Consideremos la trayectoria

$$
E\rightarrow M\rightarrow A\rightarrow A.
$$

Su probabilidad es

$$
P(E,M,A,A)
=
P(X_0=E)
P(M\mid E)
P(A\mid M)
P(A\mid A).
$$

Por tanto,

$$
P(E,M,A,A)
=
1(0.40)(0.40)(0.50)
=
0.08.
$$

Así, la probabilidad de observar exactamente esta trayectoria es $0.08$.

<br><br>

## 7. Verosimilitud de una trayectoria

La expresión anterior permite introducir una conexión fundamental entre cadenas de Markov y estadística.

Supongamos que observamos una trayectoria

$$
x_0,x_1,\ldots,x_n
$$

y que la matriz de transición depende de un conjunto de parámetros $\theta$:

$$
P=P(\theta).
$$

La **verosimilitud** de los parámetros dados los datos observados es

$$
L(\theta)
=
P_\theta(X_0=x_0,\ldots,X_n=x_n).
$$

Por la propiedad de Markov,

$$
\boxed{
L(\theta)
=
\pi_{x_0}(\theta)
\prod_{t=1}^{n}
P_{x_{t-1}x_t}(\theta)
}.
$$

La función de verosimilitud permite determinar qué valores de los parámetros hacen más probable la trayectoria observada.

<br><br>

### 7.1 Log-verosimilitud

Para facilitar los cálculos suele utilizarse el logaritmo de la verosimilitud:

$$
\ell(\theta)=\log L(\theta).
$$

Entonces,

$$
\ell(\theta)
=
\log \pi_{x_0}(\theta)
+
\sum_{t=1}^{n}
\log P_{x_{t-1}x_t}(\theta).
$$

La transformación es útil porque convierte productos en sumas y facilita los procedimientos de optimización numérica.

<br><br>

### 7.2 Estimación de las probabilidades de transición

Supongamos que observamos una trayectoria y contamos cuántas veces se produce cada transición.

Sea

$$
N_{ij}
=
\text{número de veces que se observa la transición }i\to j.
$$

El número total de transiciones que parten del estado $i$ es

$$
N_i=\sum_jN_{ij}.
$$

Una estimación natural de la probabilidad de transición es

$$
\boxed{
\widehat P_{ij}
=
\frac{N_{ij}}{N_i}
}.
$$

Esta estimación tiene una interpretación sencilla: la probabilidad de pasar de $i$ a $j$ se aproxima mediante la frecuencia relativa con la que observamos dicha transición.

<br><br>

### 7.3 Ejemplo

Supongamos que observamos las siguientes transiciones desde el estado $A$:

* $A\to A$: 50 veces.
* $A\to M$: 30 veces.
* $A\to E$: 20 veces.

Entonces,

$$
N_A=50+30+20=100.
$$

Por tanto,

$$
\widehat P_{AA}=0.50,
$$

$$
\widehat P_{AM}=0.30,
$$

y

$$
\widehat P_{AE}=0.20.
$$

Este procedimiento permite construir una matriz de transición directamente a partir de datos.

<br><br>

## 8. Clasificación de estados

El comportamiento a largo plazo de una cadena depende de la estructura de sus estados y de las posibilidades de transición entre ellos.

<br><br>

### 8.1 Comunicación entre estados

Decimos que un estado $i$ **alcanza** al estado $j$ si existe algún número $n\geq1$ tal que

$$
(P^n)_{ij}>0.
$$

Si $i$ alcanza a $j$ y $j$ alcanza a $i$, decimos que ambos estados **se comunican** y escribimos

$$
i\leftrightarrow j.
$$

La comunicación permite dividir los estados en clases de comunicación.

<br><br>

### 8.2 Cadena irreducible

Una cadena es **irreducible** si todos sus estados se comunican entre sí.

Equivalentemente, para cualquier par de estados $i$ y $j$, existe algún $n$ tal que

$$
(P^n)_{ij}>0.
$$

En una cadena irreducible, todos los estados pertenecen a una única clase de comunicación.

<br><br>

### 8.3 Estados absorbentes

Un estado $i$ es absorbente si

$$
P_{ii}=1.
$$

En consecuencia, una vez que la cadena entra en dicho estado, permanece allí indefinidamente.

Por ejemplo,

$$
P=
\begin{pmatrix}
0.7&0.3&0\\
0.2&0.8&0\\
0&0&1
\end{pmatrix}
$$

tiene un estado absorbente, el estado $3$.

<br><br>

### 8.4 Periodicidad

El período de un estado $i$ se relaciona con los tiempos en los que es posible regresar al mismo estado.

El período se define como

$$
d(i)
=
\gcd\{n\geq1:(P^n)_{ii}>0\}.
$$

Si $d(i)=1$, el estado es **aperiódico**.

En una cadena irreducible, todos los estados tienen el mismo período.

<br><br>

## 9. Distribuciones estacionarias

Una distribución de probabilidad

$$
\boldsymbol{\pi}
=
(\pi_1,\ldots,\pi_n)
$$

se denomina **distribución estacionaria** si permanece invariante después de una transición:

$$
\boxed{
\boldsymbol{\pi}P=\boldsymbol{\pi}
}
$$

y además

$$
\sum_{i=1}^n\pi_i=1,
\qquad
\pi_i\geq0.
$$

Por tanto, encontrar una distribución estacionaria consiste en resolver el sistema

$$
\boldsymbol{\pi}P=\boldsymbol{\pi}.
$$

Equivalentemente,

$$
(P^T-I)\boldsymbol{\pi}^T=0,
$$

junto con la condición de normalización.

<br><br>

### 9.1 Interpretación

Si una cadena comienza con distribución

$$
\mathbf{v}_0=\boldsymbol{\pi},
$$

entonces

$$
\mathbf{v}_1
=
\boldsymbol{\pi}P
=
\boldsymbol{\pi}.
$$

Por inducción,

$$
\mathbf{v}_n=\boldsymbol{\pi}
$$

para todo $n$.

La distribución estacionaria representa, por tanto, una distribución que permanece invariante bajo la dinámica probabilística de la cadena.

<br><br>

## 10. Punto límite y comportamiento a largo plazo

La existencia de una distribución estacionaria no implica automáticamente que todas las distribuciones iniciales converjan hacia ella.

Para estudiar el comportamiento a largo plazo debemos analizar el límite

$$
\lim_{n\to\infty}\mathbf{v}_0P^n.
$$

Cuando este límite existe y es independiente de $\mathbf{v}_0$, decimos que la cadena converge hacia una distribución límite.

<br><br>

### 10.1 Punto límite de la distribución

Supongamos que existe

$$
\lim_{n\to\infty}\mathbf{v}_0P^n
=
\boldsymbol{\pi}.
$$

Entonces $\boldsymbol{\pi}$ es una distribución estacionaria.

En efecto,

$$
\begin{aligned}
\boldsymbol{\pi}P
&=
\left(\lim_{n\to\infty}\mathbf{v}_0P^n\right)P\\
&=
\lim_{n\to\infty}\mathbf{v}_0P^{n+1}\\
&=
\boldsymbol{\pi}.
\end{aligned}
$$

Así, una distribución límite debe ser estacionaria.

<br><br>

### 10.2 Cadenas ergódicas

Para una cadena finita, irreducible y aperiódica, existe una única distribución estacionaria $\boldsymbol{\pi}$ y, además,

$$
\boxed{
\lim_{n\to\infty}P^n
=
\begin{pmatrix}
\pi_1&\cdots&\pi_n\\
\pi_1&\cdots&\pi_n\\
\vdots&\ddots&\vdots\\
\pi_1&\cdots&\pi_n
\end{pmatrix}
}.
$$

Por tanto, independientemente de la distribución inicial,

$$
\boxed{
\lim_{n\to\infty}\mathbf{v}_0P^n
=
\boldsymbol{\pi}
}.
$$

Este resultado constituye una de las razones principales por las que las cadenas de Markov son útiles para estudiar sistemas a largo plazo.

<br><br>

### 10.3 Ejemplo: comportamiento límite del modelo climático

Para la matriz

$$
P=
\begin{pmatrix}
0.7&0.2&0.1\\
0.3&0.4&0.3\\
0.2&0.3&0.5
\end{pmatrix},
$$

podemos buscar una distribución estacionaria

$$
\boldsymbol{\pi}=(\pi_S,\pi_N,\pi_L)
$$

que satisfaga

$$
\boldsymbol{\pi}P=\boldsymbol{\pi}
$$

y

$$
\pi_S+\pi_N+\pi_L=1.
$$

El sistema resultante es

$$
\begin{cases}
0.7\pi_S+0.3\pi_N+0.2\pi_L=\pi_S,\\
0.2\pi_S+0.4\pi_N+0.3\pi_L=\pi_N,\\
0.1\pi_S+0.3\pi_N+0.5\pi_L=\pi_L,\\
\pi_S+\pi_N+\pi_L=1.
\end{cases}
$$

Al resolverlo obtenemos la distribución estacionaria.

Esta distribución permite interpretar las probabilidades de los diferentes estados en el largo plazo, independientemente del estado climático inicial.

<br><br>

## 11. Interpretación espectral del comportamiento límite

La matriz de transición de una cadena de Markov posee una conexión importante con el álgebra lineal.

Como cada fila de $P$ suma uno,

$$
P\mathbf{1}=\mathbf{1},
$$

donde $\mathbf{1}$ es el vector columna cuyos componentes son todos iguales a uno. Por tanto, $1$ es un valor propio de $P$.

La distribución estacionaria, en cambio, satisface

$$
\boldsymbol{\pi}P=\boldsymbol{\pi},
$$

por lo que puede interpretarse como un vector propio izquierdo asociado al valor propio $1$.

Cuando la cadena es finita, irreducible y aperiódica, los demás valores propios tienen módulo estrictamente menor que uno. Esto explica algebraicamente la convergencia de $P^n$.

Si los valores propios de $P$ se denotan por

$$
\lambda_1,\lambda_2,\ldots,\lambda_n,
$$

entonces

$$
\lambda_1=1,
$$

mientras que, bajo las condiciones de ergodicidad,

$$
|\lambda_j|<1,
\qquad j\geq2.
$$

Por tanto, las contribuciones asociadas a los demás valores propios desaparecen cuando $n$ aumenta.

<br><br>

## 12. Simulación de cadenas de Markov

Además del análisis algebraico, las cadenas de Markov pueden estudiarse mediante simulación computacional.

Para generar una trayectoria, se selecciona un estado inicial y posteriormente se genera cada nuevo estado de acuerdo con la fila correspondiente de la matriz de transición.

Por ejemplo, podemos implementar el modelo climático mediante Python:

```python
import numpy as np
import matplotlib.pyplot as plt

P = np.array([
    [0.7, 0.2, 0.1],
    [0.3, 0.4, 0.3],
    [0.2, 0.3, 0.5]
])

estados = ["S", "N", "L"]

estado_actual = 0
trayectoria = [estado_actual]

num_pasos = 100

for _ in range(num_pasos):
    estado_actual = np.random.choice(
        len(estados),
        p=P[estado_actual]
    )
    trayectoria.append(estado_actual)

trayectoria = np.array(trayectoria)

plt.plot(trayectoria)
plt.yticks(range(len(estados)), estados)
plt.xlabel("Tiempo")
plt.ylabel("Estado")
plt.title("Trayectoria de una cadena de Markov")
plt.show()
```

La trayectoria obtenida es solamente una realización posible. Si repetimos la simulación obtendremos trayectorias diferentes, aunque todas estarán gobernadas por la misma matriz de transición.

<br><br>

## 13. Evolución de las probabilidades mediante simulación

También podemos utilizar simulaciones para aproximar la distribución estacionaria.

Supongamos que generamos una trayectoria suficientemente larga. La frecuencia relativa con la que aparece cada estado puede utilizarse como una aproximación de su probabilidad estacionaria.

Si

$$
N_i(n)
$$

es el número de veces que el estado $i$ aparece durante los primeros $n$ pasos, podemos considerar la frecuencia

$$
\widehat{\pi}_i(n)
=
\frac{N_i(n)}{n}.
$$

Para una cadena ergódica, estas frecuencias convergen hacia la distribución estacionaria:

$$
\widehat{\pi}_i(n)\longrightarrow\pi_i.
$$

Esta idea constituye una manifestación de la **ley de los grandes números para cadenas de Markov**.

<br><br>

## 14. Cadenas de Markov ocultas

En muchas aplicaciones el estado del sistema no puede observarse directamente.

Por ejemplo, podemos estar interesados en determinar el estado de salud de una persona, pero únicamente observar mediciones clínicas; o podemos querer determinar el estado climático de una región utilizando observaciones indirectas.

Para estos problemas se utilizan las **cadenas de Markov ocultas**, conocidas como **Hidden Markov Models (HMM)**.

<br><br>

### 14.1 Estructura de una cadena de Markov oculta

Una cadena de Markov oculta contiene dos procesos:

1. Un proceso de estados ocultos

$$
X_0,X_1,X_2,\ldots
$$

que satisface la propiedad de Markov.

2. Un proceso de observaciones

$$
Y_0,Y_1,Y_2,\ldots
$$

que depende probabilísticamente del estado oculto correspondiente.

La estructura puede representarse conceptualmente como

$$
X_0\longrightarrow X_1\longrightarrow X_2\longrightarrow X_3\longrightarrow\cdots
$$

con observaciones

$$
\downarrow\qquad\downarrow\qquad\downarrow\qquad\downarrow
$$

$$
Y_0\qquad Y_1\qquad Y_2\qquad Y_3\qquad\cdots
$$

<br><br>

### 14.2 Propiedad de Markov de los estados ocultos

Los estados ocultos satisfacen

$$
P(X_{t+1}\mid X_t,X_{t-1},\ldots,X_0)
=
P(X_{t+1}\mid X_t).
$$

Por otra parte, las observaciones satisfacen la propiedad de que

$$
P(Y_t\mid X_t,X_{t-1},\ldots,Y_{t-1})
=
P(Y_t\mid X_t).
$$

Es decir, una vez conocido el estado oculto $X_t$, la observación $Y_t$ no necesita información adicional de los estados u observaciones anteriores.

<br><br>

### 14.3 Elementos de un HMM

Un modelo oculto de Markov puede especificarse mediante tres componentes principales:

**Distribución inicial**

$$
\boldsymbol{\pi}
$$

que determina la probabilidad del estado oculto inicial.

**Matriz de transición**

$$
P_{ij}
=
P(X_{t+1}=j\mid X_t=i).
$$

**Matriz o distribución de emisión**

$$
B_{ij}
=
P(Y_t=j\mid X_t=i).
$$

La matriz de emisión describe cómo los estados ocultos generan las observaciones.

<br><br>

### 14.4 Ejemplo conceptual

Supongamos que queremos modelar el clima de una región, pero no podemos observar directamente el estado climático real. En cambio, observamos si una persona lleva paraguas.

Los estados ocultos pueden ser

$$
X_t\in\{\text{Soleado},\text{Lluvioso}\},
$$

mientras que las observaciones pueden ser

$$
Y_t\in\{\text{Paraguas},\text{No paraguas}\}.
$$

Podemos tener una matriz de transición

$$
P=
\begin{pmatrix}
0.8&0.2\\
0.3&0.7
\end{pmatrix}
$$

y una matriz de emisión

$$
B=
\begin{pmatrix}
0.1&0.9\\
0.8&0.2
\end{pmatrix}.
$$

La primera fila de $B$ indica que cuando el clima es soleado existe una probabilidad de $0.1$ de observar un paraguas y una probabilidad de $0.9$ de no observarlo.

La segunda fila indica que cuando está lloviendo existe una probabilidad de $0.8$ de observar un paraguas.

<br><br>

## 15. Problemas fundamentales de las cadenas de Markov ocultas

Los HMM plantean tres problemas fundamentales.

### 15.1 Evaluación

Dada una secuencia de observaciones

$$
y_0,y_1,\ldots,y_n,
$$

queremos calcular

$$
P(Y_0=y_0,\ldots,Y_n=y_n).
$$

Este problema puede resolverse eficientemente mediante el **algoritmo hacia adelante** (*forward algorithm*).

<br><br>

### 15.2 Decodificación

Dada una secuencia observada

$$
y_0,y_1,\ldots,y_n,
$$

queremos determinar la trayectoria de estados ocultos más probable:

$$
x_0^*,x_1^*,\ldots,x_n^*.
$$

Este problema se resuelve mediante el **algoritmo de Viterbi**.

<br><br>

### 15.3 Estimación de parámetros

Finalmente, podemos tener observaciones pero desconocer los parámetros del modelo, es decir, la matriz de transición, las probabilidades de emisión o la distribución inicial.

En este caso debemos estimar los parámetros a partir de los datos. Uno de los procedimientos clásicos es el algoritmo **Baum-Welch**, basado en una aplicación del algoritmo EM.

<br><br>

## 16. Relación entre cadenas de Markov y modelos estadísticos

Las cadenas de Markov proporcionan una conexión natural entre modelos dinámicos y estadística.

En un modelo determinista podemos escribir una evolución como

$$
x_{t+1}=f(x_t).
$$

En una cadena de Markov, esta evolución se reemplaza por una distribución:

$$
P(X_{t+1}=j\mid X_t=i)=P_{ij}.
$$

Así, en lugar de preguntar cuál será exactamente el siguiente estado, preguntamos cuál es la probabilidad de cada posible estado.

Además, cuando disponemos de datos podemos utilizar las trayectorias observadas para estimar los parámetros del modelo.

De esta manera se establece un ciclo fundamental:

$$
\boxed{
\text{datos}
\longrightarrow
\text{modelo probabilístico}
\longrightarrow
\text{predicción}
\longrightarrow
\text{comparación con los datos}
}
$$

Este principio constituye una de las ideas fundamentales del modelamiento estadístico y estocástico.

<br><br>

## 17. Ejemplo completo: dinámica de una población

Consideremos una población que puede clasificarse en tres estados:

* $A$: población abundante.
* $M$: población moderada.
* $E$: población escasa.

A partir de observaciones históricas se obtiene la siguiente tabla de transiciones:

| Estado actual | Abundante | Moderada | Escasa |
| ------------- | --------: | -------: | -----: |
| Abundante     |        50 |       30 |     20 |
| Moderada      |        40 |       50 |     10 |
| Escasa        |        30 |       40 |     30 |

La matriz de transición se obtiene dividiendo cada fila por su suma:

$$
P=
\begin{pmatrix}
0.50&0.30&0.20\\
0.40&0.50&0.10\\
0.30&0.40&0.30
\end{pmatrix}.
$$

Supongamos que inicialmente la población es escasa:

$$
\mathbf{v}_0=(0,0,1).
$$

Después de una semana,

$$
\mathbf{v}_1
=
\mathbf{v}_0P.
$$

Después de siete semanas,

$$
\mathbf{v}_7
=
\mathbf{v}_0P^7.
$$

Podemos calcular esta distribución mediante Python:

```python
import numpy as np

P = np.array([
    [0.50, 0.30, 0.20],
    [0.40, 0.50, 0.10],
    [0.30, 0.40, 0.30]
])

v0 = np.array([0, 0, 1])

v7 = v0 @ np.linalg.matrix_power(P, 7)

print("Distribución después de 7 pasos:")
print(v7)
```

Este procedimiento permite determinar las probabilidades de encontrar la población en cada uno de los tres estados después de siete pasos.

<br><br>

## 18. Ideas principales

En este capítulo hemos introducido los conceptos fundamentales necesarios para construir modelos estocásticos basados en cadenas de Markov.

Las ideas principales son:

1. Un fenómeno aleatorio puede representarse mediante un espacio muestral y una distribución de probabilidad.

2. Una variable aleatoria permite representar numéricamente los resultados de un experimento aleatorio.

3. Un proceso estocástico es una colección de variables aleatorias indexadas por el tiempo.

4. Una cadena de Markov es un proceso estocástico que satisface la propiedad de Markov.

5. En una cadena de Markov homogénea en tiempo discreto, las probabilidades de transición pueden representarse mediante una matriz $P$.

6. La distribución de los estados evoluciona mediante

$$
\mathbf{v}_{n+1}=\mathbf{v}_nP.
$$

7. La distribución después de $n$ pasos está dada por

$$
\mathbf{v}_n=\mathbf{v}_0P^n.
$$

8. Una trayectoria es una realización particular de la cadena.

9. La probabilidad de una trayectoria puede calcularse mediante

$$
P(X_0=x_0,\ldots,X_n=x_n)
=
\pi_{x_0}
\prod_{t=1}^{n}P_{x_{t-1}x_t}.
$$

10. Esta expresión permite construir la función de verosimilitud y estimar las probabilidades de transición a partir de datos.

11. Una distribución estacionaria satisface

$$
\boldsymbol{\pi}P=\boldsymbol{\pi}.
$$

12. Bajo condiciones apropiadas, como irreducibilidad y aperiodicidad en una cadena finita, la distribución de los estados converge hacia una distribución estacionaria.

13. Las cadenas de Markov ocultas permiten modelar situaciones en las que los estados del sistema no pueden observarse directamente.

14. En un HMM, las observaciones dependen probabilísticamente de los estados ocultos.

15. Los principales problemas de los HMM son la evaluación, la decodificación y la estimación de parámetros.

<br><br>

## 19. Ejercicios

### Ejercicio 1

Se lanza un dado justo.

1. Defina el espacio muestral.
2. Defina el evento correspondiente a obtener un número par.
3. Calcule la probabilidad del evento.
4. Calcule la probabilidad de obtener un número mayor que $4$.
5. Determine la probabilidad de obtener un número par o mayor que $4$.

<br><br>

### Ejercicio 2

Una moneda justa se lanza cinco veces. Defina $X$ como el número de caras obtenidas.

1. Determine los posibles valores de $X$.
2. Calcule $P(X=k)$ para cada valor posible de $k$.
3. Calcule $P(X\geq3)$.
4. Calcule $E[X]$.

<br><br>

### Ejercicio 3

Una población contiene $100$ individuos, de los cuales $40$ presentan una determinada característica. Se seleccionan $10$ individuos sin reposición.

1. Defina una variable aleatoria para representar el número de individuos con la característica.
2. Determine la distribución de probabilidad apropiada.
3. Calcule la probabilidad de seleccionar exactamente cuatro individuos con la característica.
4. Calcule la probabilidad de seleccionar al menos tres.

<br><br>

### Ejercicio 4

Considere la matriz de transición

$$
P=
\begin{pmatrix}
0.8&0.2\\
0.4&0.6
\end{pmatrix}.
$$

1. Verifique que $P$ es una matriz de transición.
2. Si $\mathbf{v}_0=(1,0)$, calcule $\mathbf{v}_1$, $\mathbf{v}_2$ y $\mathbf{v}_3$.
3. Calcule $P^5$.
4. Determine la distribución estacionaria.

<br><br>

### Ejercicio 5

Considere una cadena con estados $A$, $B$ y $C$ y matriz

$$
P=
\begin{pmatrix}
0.5&0.3&0.2\\
0.2&0.6&0.2\\
0.1&0.3&0.6
\end{pmatrix}.
$$

Determine la probabilidad de observar la trayectoria

$$
A\rightarrow B\rightarrow C\rightarrow C\rightarrow A.
$$

<br><br>

### Ejercicio 6

Considere la trayectoria

$$
A,A,B,A,C,B,B,A.
$$

1. Cuente el número de transiciones de cada tipo.
2. Construya los valores $N_{ij}$.
3. Estime la matriz de transición utilizando

$$
\widehat P_{ij}
=
\frac{N_{ij}}{\sum_jN_{ij}}.
$$

<br><br>

### Ejercicio 7

Para una cadena de Markov con matriz

$$
P=
\begin{pmatrix}
0.7&0.3&0\\
0.2&0.8&0\\
0&0&1
\end{pmatrix},
$$

1. Identifique los estados absorbentes.
2. Determine las clases de comunicación.
3. Determine si la cadena es irreducible.
4. Analice el comportamiento a largo plazo.

<br><br>

### Ejercicio 8

Considere la matriz

$$
P=
\begin{pmatrix}
0.6&0.4\\
0.2&0.8
\end{pmatrix}.
$$

1. Encuentre la distribución estacionaria.
2. Calcule $P^n$ para varios valores de $n$.
3. Observe numéricamente qué ocurre cuando $n$ aumenta.
4. Compare el resultado con la distribución estacionaria.

<br><br>

### Ejercicio 9

Escriba un programa en Python que simule una trayectoria de una cadena de Markov durante $1000$ pasos.

1. Grafique la trayectoria.
2. Calcule la frecuencia relativa de cada estado.
3. Calcule la distribución estacionaria mediante $\boldsymbol{\pi}P=\boldsymbol{\pi}$.
4. Compare ambas cantidades.

<br><br>

### Ejercicio 10

Considere un modelo oculto de Markov con dos estados ocultos:

$$
X_t\in\{1,2\},
$$

y dos posibles observaciones:

$$
Y_t\in\{A,B\}.
$$

Suponga que

$$
P=
\begin{pmatrix}
0.8&0.2\\
0.3&0.7
\end{pmatrix}
$$

y

$$
B=
\begin{pmatrix}
0.7&0.3\\
0.2&0.8
\end{pmatrix}.
$$

1. Interprete las matrices $P$ y $B$.
2. Calcule la probabilidad de una trayectoria particular de estados y observaciones.
3. Determine cuál de las dos observaciones es más probable en cada estado.
4. Explique conceptualmente cómo podría utilizarse el algoritmo de Viterbi para reconstruir la trayectoria de estados ocultos.

<br><br>

### Ejercicio 11

Considere una cadena de Markov con tres estados y una trayectoria observada de longitud $n$.

Demuestre que la log-verosimilitud de la trayectoria puede escribirse como

$$
\ell
=
\log\pi_{x_0}
+
\sum_{t=1}^{n}
\log P_{x_{t-1}x_t}.
$$

Explique por qué esta representación resulta más conveniente que trabajar directamente con la verosimilitud.

<br><br>

### Ejercicio 12

Utilice simulación computacional para investigar experimentalmente la convergencia de una cadena de Markov hacia su distribución estacionaria.

Considere varias distribuciones iniciales diferentes y determine si todas convergen hacia la misma distribución.

Discuta qué propiedades de la matriz de transición parecen ser necesarias para que esta convergencia ocurra.
