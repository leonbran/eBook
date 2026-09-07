# Modelos de cambio discreto

## Introducción

En muchos fenómenos científicos, el estado de un sistema no se observa de manera continua, sino en instantes separados de tiempo. Por ejemplo, podemos registrar una población una vez por año, el número de individuos de una colonia bacteriana cada hora, la concentración de una sustancia cada minuto o el número de personas infectadas al final de cada día.

En estos casos resulta natural describir la evolución del sistema mediante una sucesión de estados

$$
x_0,x_1,x_2,\ldots
$$

donde $x_n$ representa el estado del sistema en el instante discreto $n$.

La idea fundamental de un modelo de cambio discreto es describir cómo se obtiene el estado siguiente a partir del estado actual:

$$
\boxed{\text{estado actual} \longrightarrow \text{regla de evolución} \longrightarrow \text{estado siguiente}}
$$

Matemáticamente, esto conduce de manera natural a modelos de la forma

$$
x_{n+1}=f(x_n).
$$

Este tipo de ecuaciones aparece en numerosos campos de la ciencia. Algunos ejemplos son:

* crecimiento de poblaciones;
* dinámica de especies;
* propagación de enfermedades;
* evolución de concentraciones químicas;
* modelos económicos;
* procesos financieros;
* dinámica de poblaciones celulares;
* simulación numérica de sistemas físicos.

En este capítulo estudiaremos las herramientas matemáticas necesarias para construir y analizar estos modelos.

La idea central será que una regla aparentemente sencilla de evolución puede generar comportamientos muy diferentes dependiendo de la función $f$, de los parámetros y del estado inicial. Por esta razón, construir un modelo discreto no consiste únicamente en calcular términos de una sucesión: también debemos comprender la dinámica que genera la regla de evolución.

## 1. Fundamentos matemáticos: sucesiones

### 1.1 ¿Qué son las sucesiones?

Una sucesión es una lista ordenada de números

$$
x_0,x_1,x_2,\ldots
$$

que podemos representar mediante la notación

$$
\{x_n\}_{n=0}^{\infty}.
$$

El subíndice $n$ permite identificar la posición de cada término dentro de la sucesión.

En el contexto del modelamiento matemático, podemos interpretar $n$ como un índice temporal. Así,

$$
x_n
$$

representa el estado del sistema en el instante $n$.

Por ejemplo, si $x_n$ representa el número de individuos de una población medido cada año, entonces:

$$
x_0=\text{población inicial},
$$

$$
x_1=\text{población después de un año},
$$

$$
x_2=\text{población después de dos años},
$$

y así sucesivamente.

Esta interpretación convierte una sucesión matemática en una descripción de la evolución de un fenómeno.

Es importante notar que el índice $n$ no necesariamente representa años. Puede representar horas, días, generaciones, periodos financieros, pasos computacionales o cualquier otra unidad temporal apropiada para el problema.

### 1.2 Sucesiones definidas explícitamente

Una sucesión puede definirse mediante una fórmula que permite calcular directamente cualquier término.

Por ejemplo,

$$
x_n=2n+1.
$$

Los primeros términos son

$$
x_0=1,\qquad
x_1=3,\qquad
x_2=5,\qquad
x_3=7.
$$

En general, para obtener $x_n$ no necesitamos conocer los términos anteriores.

Este tipo de expresión se denomina una **fórmula explícita**.

Por ejemplo, si queremos calcular el término correspondiente a $n=100$, basta con sustituir:

$$
x_{100}=2(100)+1=201.
$$

Las fórmulas explícitas son particularmente útiles cuando se desea estudiar el comportamiento de una sucesión sin tener que calcular todos sus términos anteriores.

### 1.3 Sucesiones como modelos de evolución

Consideremos una población bacteriana que inicialmente contiene $100$ bacterias y que se duplica cada hora.

Después de una hora tendremos

$$
x_1=2x_0.
$$

Después de dos horas,

$$
x_2=2x_1=2^2x_0.
$$

Continuando de esta manera,

$$
x_n=100(2)^n.
$$

La sucesión

$$
x_n=100(2)^n
$$

es entonces un modelo matemático de la evolución de la población.

Este ejemplo muestra que una sucesión puede representar mucho más que una lista de números: puede representar el estado de un sistema a lo largo del tiempo.

También muestra una diferencia importante entre una **observación** y un **modelo**. Si medimos experimentalmente la población cada hora, obtenemos datos. Si suponemos que la población se duplica exactamente en cada intervalo, estamos construyendo un modelo que intenta explicar o aproximar esos datos.

### 1.4 Comportamiento de una sucesión

Al estudiar una sucesión asociada a un fenómeno científico, no solamente nos interesa calcular sus términos. También queremos entender su comportamiento.

Una sucesión puede:

* crecer;
* decrecer;
* permanecer constante;
* converger a un valor;
* divergir;
* oscilar.

Por ejemplo,

$$
x_n=2^n
$$

crece sin límite, mientras que

$$
x_n=\left(\frac12\right)^n
$$

converge a cero.

En cambio,

$$
x_n=(-1)^n
$$

oscila entre $1$ y $-1$.

Otro ejemplo es

$$
x_n=3+\left(\frac12\right)^n.
$$

En este caso,

$$
x_n\longrightarrow3
$$

cuando $n\to\infty$.

La identificación de estos comportamientos será fundamental para interpretar modelos de cambio discreto.

## 2. Sucesiones recurrentes

### 2.1 ¿Qué es una sucesión recurrente?

En muchos modelos científicos no conocemos directamente una fórmula para $x_n$. En cambio, conocemos una regla que permite obtener el estado siguiente a partir del estado actual.

Una sucesión recurrente tiene la forma

$$
x_{n+1}=f(x_n),
$$

acompañada de una condición inicial

$$
x_0=x_{\mathrm{ini}}.
$$

La condición inicial indica dónde comienza el sistema, mientras que la ecuación recurrente indica cómo evoluciona.

Podemos interpretar el modelo como

$$
x_0
\longrightarrow
x_1
\longrightarrow
x_2
\longrightarrow
x_3
\longrightarrow\cdots
$$

donde

$$
x_{n+1}=f(x_n).
$$

Esta estructura es una de las ideas centrales de los modelos de cambio discreto.

Por ejemplo, si

$$
x_{n+1}=2x_n,
\qquad x_0=3,
$$

entonces

$$
x_1=6,\qquad
x_2=12,\qquad
x_3=24.
$$

La regla de evolución y la condición inicial determinan completamente la trayectoria.

### 2.2 Ejemplo: crecimiento financiero

Supongamos que una inversión inicial es $P_0$ y que cada periodo aumenta en una tasa $r$.

El incremento durante un periodo es

$$
rP_n.
$$

Por tanto,

$$
P_{n+1}=P_n+rP_n.
$$

Factorizando,

$$
P_{n+1}=(1+r)P_n.
$$

Por ejemplo, si una inversión crece un $5%$ por periodo,

$$
P_{n+1}=1.05P_n.
$$

Si inicialmente

$$
P_0=1000,
$$

entonces

$$
P_1=1050,
$$

$$
P_2=1102.50,
$$

$$
P_3=1157.625.
$$

En este caso también podemos obtener una fórmula explícita:

$$
P_n=P_0(1+r)^n.
$$

Este modelo permite observar una característica importante del crecimiento compuesto: el incremento absoluto aumenta con el tiempo aunque la tasa porcentual permanezca constante.

### 2.3 Ejemplo: reproducción de una población

Supongamos que una población tiene $N_n$ individuos en la generación $n$ y que cada generación produce, en promedio, $R$ veces la población anterior.

Entonces

$$
N_{n+1}=RN_n.
$$

Si $R>1$, la población crece.

Si $0<R<1$, la población disminuye.

Si $R=1$, la población permanece constante.

La solución explícita es

$$
N_n=N_0R^n.
$$

Este modelo es una primera aproximación a procesos de reproducción y constituye la base para modelos poblacionales más realistas.

Es importante interpretar $R$ correctamente. Por ejemplo, si $R=1.2$, esto significa que cada generación tiene, en promedio, el $120%$ de la población de la generación anterior, es decir, un crecimiento del $20%$ por generación.

## 3. Ecuaciones en diferencias

### 3.1 Cambio discreto

En un modelo discreto, el cambio entre dos instantes consecutivos se expresa mediante

$$
x_{n+1}-x_n.
$$

Esta expresión se denomina una **diferencia finita**.

Por ejemplo, si una población pasa de

$$
x_n=1000
$$

a

$$
x_{n+1}=1200,
$$

el cambio durante ese periodo es

$$
x_{n+1}-x_n=200.
$$

La diferencia relativa es

$$
\frac{x_{n+1}-x_n}{x_n}
=
\frac{200}{1000}
=
0.2.
$$

Es decir, la población aumentó un $20%$.

Cuando los intervalos temporales tienen una duración $\Delta t$, podemos considerar también la tasa de cambio discreta

$$
\frac{x_{n+1}-x_n}{\Delta t}.
$$

Esta cantidad representa el cambio promedio por unidad de tiempo durante el intervalo considerado.

### 3.2 Ecuaciones en diferencias

Una ecuación en diferencias es una ecuación que relaciona diferentes términos de una sucesión.

Por ejemplo,

$$
x_{n+1}-x_n=rx_n.
$$

Reorganizando,

$$
x_{n+1}=(1+r)x_n.
$$

Por tanto, la ecuación en diferencias describe directamente la regla de evolución del sistema.

También pueden aparecer modelos que dependan de varios estados anteriores. Por ejemplo,

$$
x_{n+1}-2x_n+x_{n-1}=0.
$$

En este caso, el nuevo estado depende de los dos estados anteriores.

Las ecuaciones en diferencias permiten construir modelos considerablemente más generales que las recurrencias de primer orden.

Una diferencia importante es que una recurrencia de primer orden como

$$
x_{n+1}=f(x_n)
$$

requiere normalmente una condición inicial $x_0$, mientras que una ecuación que involucra dos estados anteriores, como

$$
x_{n+1}=2x_n-x_{n-1},
$$

requiere conocer dos condiciones iniciales, por ejemplo $x_0$ y $x_1$.

### 3.3 Diferencias finitas y derivadas

Existe una conexión importante entre modelos discretos y modelos continuos.

La derivada de una función $x(t)$ se define mediante el límite

$$
\frac{dx}{dt}
=
\lim_{\Delta t\to0}
\frac{x(t+\Delta t)-x(t)}{\Delta t}.
$$

En un modelo discreto podemos utilizar la aproximación

$$
\frac{x_{n+1}-x_n}{\Delta t}
\approx
\frac{dx}{dt}.
$$

Por tanto,

$$
x_{n+1}-x_n
$$

puede interpretarse como una aproximación discreta del cambio continuo.

Esta conexión será fundamental cuando pasemos posteriormente de los modelos discretos a las ecuaciones diferenciales.

### 3.4 Ejemplo: crecimiento proporcional

Supongamos que una cantidad $x_n$ cambia proporcionalmente a su tamaño actual.

Podemos escribir

$$
x_{n+1}-x_n=rx_n.
$$

Entonces,

$$
x_{n+1}=(1+r)x_n.
$$

Este mismo principio aparece en muchos contextos:

* crecimiento poblacional;
* reproducción bacteriana;
* interés compuesto;
* depreciación;
* crecimiento de inversiones;
* desintegración radiactiva aproximada;
* disminución de concentraciones.

Una misma estructura matemática puede representar fenómenos completamente diferentes.

Por ejemplo, si $r=-0.1$, obtenemos

$$
x_{n+1}=0.9x_n,
$$

que representa una disminución del $10%$ en cada periodo.

Así, el signo y el valor de $r$ determinan cualitativamente la dinámica del modelo.

## 4. Método de punto fijo

### 4.1 ¿Qué es un punto fijo?

Consideremos el modelo

$$
x_{n+1}=f(x_n).
$$

Un punto fijo es un valor $x^*$ que permanece constante bajo la regla de evolución:

$$
f(x^*)=x^*.
$$

Por tanto, para encontrar los puntos fijos debemos resolver

$$
f(x)=x.
$$

Si el sistema alcanza exactamente un punto fijo, entonces

$$
x_n=x^*
$$

para todo $n$.

Un punto fijo representa, por tanto, un estado que no cambia bajo la dinámica.

### 4.2 Ejemplo

Consideremos el modelo

$$
x_{n+1}=\frac12x_n+2.
$$

Busquemos sus puntos fijos.

Debemos resolver

$$
x^*=\frac12x^*+2.
$$

Por tanto,

$$
\frac12x^*=2,
$$

y obtenemos

$$
x^*=4.
$$

El valor $4$ es un estado de equilibrio del sistema.

Podemos comprobarlo directamente:

$$
f(4)=\frac12(4)+2=4.
$$

Por tanto, si comenzamos exactamente con $x_0=4$, obtenemos

$$
x_1=x_2=x_3=\cdots=4.
$$

### 4.3 Interpretación científica

Un punto fijo representa un estado que no cambia bajo la dinámica del modelo.

Por ejemplo, podría representar:

* una población estable;
* una concentración de equilibrio;
* una temperatura estacionaria;
* un nivel constante de recursos;
* un estado estacionario de un sistema económico.

Sin embargo, encontrar un punto fijo no nos dice todavía si el sistema realmente se aproxima a él.

Para responder esta pregunta necesitamos estudiar su estabilidad.

## 5. Equilibrios y estabilidad

### 5.1 ¿Qué significa que un equilibrio sea estable?

Supongamos nuevamente

$$
x_{n+1}=f(x_n)
$$

y que $x^*$ es un punto fijo.

Una pregunta fundamental es:

> ¿Qué sucede si comenzamos cerca de $x^*$?

Si las iteraciones permanecen cerca del equilibrio y, en particular, si se aproximan a él, decimos que el equilibrio es **localmente estable**. Si las trayectorias cercanas se alejan del equilibrio, este es **inestable**.

Por ejemplo,

$$
x_{n+1}=\frac12x_n+2.
$$

Sabemos que

$$
x^*=4.
$$

Si comenzamos con

$$
x_0=5,
$$

obtenemos

$$
x_1=4.5,
$$

$$
x_2=4.25,
$$

$$
x_3=4.125,
$$

y las iteraciones continúan acercándose a $4$.

Por tanto, $x^*=4$ es un equilibrio estable y, en este caso, atractor.

### 5.2 Criterio de estabilidad local

Para un modelo diferenciable

$$
x_{n+1}=f(x_n),
$$

podemos estudiar la estabilidad local de un punto fijo mediante la derivada.

Si

$$
|f'(x^*)|<1,
$$

el punto fijo es localmente estable.

Si

$$
|f'(x^*)|>1,
$$

el punto fijo es localmente inestable.

Cuando

$$
|f'(x^*)|=1,
$$

el criterio no permite determinar por sí solo la estabilidad y es necesario realizar un análisis adicional.

Este resultado proporciona una conexión importante entre el comportamiento cualitativo del modelo y una propiedad matemática de la función que define la dinámica.

### 5.3 Interpretación

La derivada

$$
f'(x^*)
$$

mide, localmente, cómo se amplifican las pequeñas perturbaciones alrededor del equilibrio.

Si una perturbación $\delta_n$ satisface aproximadamente

$$
\delta_{n+1}\approx f'(x^*)\delta_n,
$$

entonces

$$
|\delta_{n+1}|
\approx
|f'(x^*)||\delta_n|.
$$

Por ello, cuando

$$
|f'(x^*)|<1,
$$

las perturbaciones disminuyen progresivamente.

El signo de $f'(x^*)$ también contiene información. Si

$$
0<f'(x^*)<1,
$$

la trayectoria tiende a aproximarse al equilibrio sin cambiar de lado en cada iteración. En cambio, si

$$
-1<f'(x^*)<0,
$$

la trayectoria suele alternar alrededor del equilibrio mientras se aproxima a él.

Por ejemplo, consideremos

$$
x_{n+1}=-\frac12x_n+6.
$$

El punto fijo satisface

$$
x^*=-\frac12x^*+6,
$$

de donde

$$
x^*=4.
$$

Además,

$$
f'(x)=-\frac12.
$$

Como

$$
|f'(4)|=\frac12<1,
$$

el equilibrio es estable. Sin embargo, debido al signo negativo de la derivada, las iteraciones oscilan alrededor de $4$.

## 6. Modelos de cambio discreto

La estructura general de un modelo de cambio discreto de primer orden puede escribirse como

$$
x_{n+1}=f(x_n),
$$

junto con una condición inicial

$$
x_0=x_{\mathrm{ini}}.
$$

Un modelo completo contiene, por tanto, dos elementos:

1. **Estado inicial**

$$
x_0=x_{\mathrm{ini}}.
$$

2. **Regla de evolución**

$$
x_{n+1}=f(x_n).
$$

La combinación de ambos permite generar la trayectoria

$$
x_0,x_1,x_2,\ldots
$$

del sistema.

Desde el punto de vista computacional, esta estructura es particularmente importante porque puede convertirse directamente en un algoritmo iterativo.

Desde el punto de vista de la modelación, también es importante distinguir tres niveles:

$$
\boxed{
\text{fenómeno}
\longrightarrow
\text{modelo matemático}
\longrightarrow
\text{trayectoria}
}
$$

El fenómeno corresponde al sistema que queremos estudiar. El modelo matemático traduce algunas de sus características en variables, parámetros y reglas de evolución. Finalmente, la trayectoria

$$
\{x_n\}
$$

representa la evolución predicha por el modelo.

## 7. Modelo de crecimiento exponencial

### 7.1 Construcción del modelo

Supongamos que una población aumenta proporcionalmente a su tamaño actual.

El cambio durante un periodo es

$$
x_{n+1}-x_n=rx_n.
$$

Entonces,

$$
x_{n+1}=(1+r)x_n.
$$

Si definimos

$$
R=1+r,
$$

obtenemos

$$
x_{n+1}=Rx_n.
$$

La solución es

$$
x_n=x_0R^n.
$$

Este modelo se conoce como **modelo de crecimiento exponencial discreto**.

### 7.2 Ejemplo: crecimiento bacteriano

Supongamos una población inicial de

$$
N_0=1000
$$

bacterias y una tasa de crecimiento del $20%$ por hora.

Entonces

$$
r=0.2,
$$

y el modelo es

$$
N_{n+1}=1.2N_n.
$$

La solución explícita es

$$
N_n=1000(1.2)^n.
$$

Después de $5$ horas,

$$
N_5=1000(1.2)^5.
$$

Calculando,

$$
N_5\approx2488.32.
$$

El modelo predice aproximadamente $2488$ bacterias después de cinco horas.

El modelo puede simularse mediante un algoritmo:

```python
N = 1000
r = 0.2

for n in range(10):
    print(n, N)
    N = (1 + r) * N
```

La estructura del código reproduce directamente la ecuación matemática.

### 7.3 Interpretación científica

El modelo exponencial supone que la tasa de crecimiento por individuo permanece constante.

Esta hipótesis puede ser razonable durante etapas tempranas de algunos procesos, cuando todavía existen suficientes recursos.

Sin embargo, una población real normalmente encuentra restricciones:

* alimento limitado;
* espacio limitado;
* competencia;
* depredación;
* enfermedades;
* cambios ambientales.

Estas restricciones motivan modelos más realistas.

Una manera sencilla de reconocer las limitaciones del modelo es observar que, si $r>0$,

$$
N_n=N_0(1+r)^n\longrightarrow\infty.
$$

Por tanto, el modelo exponencial predice crecimiento ilimitado. Esta predicción puede ser útil durante un intervalo de tiempo, pero generalmente no puede mantenerse indefinidamente en una población real.

## 8. Modelo logístico discreto

### 8.1 Incorporación de una capacidad de carga

Supongamos que una población no puede crecer indefinidamente debido a la disponibilidad limitada de recursos.

Introducimos un parámetro $K$, denominado **capacidad de carga**.

Un modelo logístico discreto sencillo es

$$
N_{n+1}
=
N_n+rN_n\left(1-\frac{N_n}{K}\right).
$$

Los parámetros son:

* $N_n$: tamaño de la población;
* $r$: tasa de crecimiento;
* $K$: capacidad de carga.

El factor

$$
1-\frac{N_n}{K}
$$

modifica el crecimiento dependiendo del tamaño actual de la población.

### 8.2 Interpretación del modelo

Cuando

$$
N_n\ll K,
$$

tenemos aproximadamente

$$
1-\frac{N_n}{K}\approx1.
$$

Por tanto,

$$
N_{n+1}\approx(1+r)N_n,
$$

y la dinámica se aproxima al crecimiento exponencial.

Cuando

$$
N_n\approx K,
$$

el término

$$
1-\frac{N_n}{K}
$$

se aproxima a cero, por lo que el crecimiento disminuye.

Así, el modelo incorpora una retroalimentación negativa:

$$
\text{mayor población}
\longrightarrow
\text{menor crecimiento relativo}.
$$

### 8.3 Equilibrios del modelo logístico

Los equilibrios satisfacen

$$
N^*
=
N^*
+
rN^*
\left(1-\frac{N^*}{K}\right).
$$

Restando $N^*$,

$$
rN^*
\left(1-\frac{N^*}{K}\right)=0.
$$

Por tanto, los puntos fijos son

$$
N_1^*=0
$$

y

$$
N_2^*=K.
$$

Estos dos equilibrios tienen interpretaciones diferentes:

* $N^*=0$: extinción;
* $N^*=K$: población en equilibrio con los recursos disponibles.

### 8.4 Ejemplo: una población que se estabiliza

Consideremos

$$
N_{n+1}
=
N_n+0.2N_n
\left(1-\frac{N_n}{500}\right),
$$

con

$$
N_0=20.
$$

Inicialmente,

$$
N_1
=
20+0.2(20)\left(1-\frac{20}{500}\right)
=
21.92.
$$

Después,

$$
N_2
=
21.92+
0.2(21.92)
\left(1-\frac{21.92}{500}\right).
$$

Continuando el proceso, la población aumenta, pero el crecimiento se hace progresivamente menor a medida que $N_n$ se aproxima a $500$.

Este comportamiento contrasta con el modelo exponencial. En el modelo logístico, la capacidad de carga limita el crecimiento.

### 8.5 Simulación

Podemos implementar el modelo en Python:

```python
import numpy as np
import matplotlib.pyplot as plt

N0 = 20
r = 0.3
K = 100

num_steps = 50

N = np.zeros(num_steps + 1)
N[0] = N0

for n in range(num_steps):
    N[n + 1] = N[n] + r * N[n] * (1 - N[n] / K)

plt.plot(N)
plt.xlabel("Tiempo")
plt.ylabel("Población")
plt.grid()
plt.show()
```

La simulación permite observar cómo la población evoluciona desde su estado inicial hacia un comportamiento cercano a la capacidad de carga.

### 8.6 El papel de los parámetros

Una de las ventajas de los modelos matemáticos es que permiten estudiar cómo cambia el comportamiento del sistema cuando modificamos sus parámetros.

En el modelo logístico,

$$
N_{n+1}
=
N_n+rN_n
\left(1-\frac{N_n}{K}\right),
$$

los parámetros $r$ y $K$ tienen papeles diferentes.

El parámetro $K$ determina la escala característica de la población, mientras que $r$ controla la intensidad del crecimiento.

Para valores pequeños de $r$, el comportamiento suele ser suave y convergente. Para valores mayores, la dinámica puede presentar oscilaciones y comportamientos cualitativamente más complejos.

El estudio detallado de estos fenómenos pertenece a una teoría más avanzada de sistemas dinámicos discretos.

Este ejemplo muestra una idea fundamental del modelamiento: **la misma ecuación puede producir comportamientos cualitativamente diferentes dependiendo de sus parámetros**.

## 9. Modelos discretos en ciencias

Los modelos de cambio discreto aparecen en numerosas disciplinas científicas.

### 9.1 Biología y ecología

Los modelos poblacionales constituyen una de las aplicaciones más naturales.

Por ejemplo,

$$
N_{n+1}=f(N_n)
$$

puede representar el tamaño de una población en la generación $n+1$ en función de la población de la generación anterior.

También podemos utilizar modelos para estudiar:

* crecimiento bacteriano;
* poblaciones de insectos;
* especies en competencia;
* recursos naturales;
* poblaciones de peces;
* regeneración de ecosistemas.

Una ventaja de los modelos discretos en ecología es que muchas poblaciones se reproducen en generaciones relativamente bien definidas. En estos casos, el índice $n$ puede representar directamente la generación.

### 9.2 Epidemiología

Durante las primeras etapas de una epidemia, cuando la población susceptible es grande, el número de individuos infectados puede crecer aproximadamente de manera exponencial.

Un modelo extremadamente sencillo sería

$$
I_{n+1}=(1+r)I_n.
$$

Sin embargo, este modelo no representa adecuadamente una epidemia completa porque ignora individuos susceptibles, recuperados y otros mecanismos epidemiológicos.

Una estructura más realista puede separar la población en diferentes grupos.

Por ejemplo,

$$
S_n=\text{susceptibles},
$$

$$
I_n=\text{infectados},
$$

$$
R_n=\text{recuperados}.
$$

Esto conduce naturalmente a modelos discretos acoplados.

Una ventaja de esta representación es que permite incorporar mecanismos como el contacto entre susceptibles e infectados, la recuperación y la pérdida de inmunidad.

### 9.3 Química

Supongamos que una sustancia se degrada y que en cada intervalo de tiempo desaparece una fracción $r$ de la cantidad presente.

Entonces,

$$
C_{n+1}=C_n-rC_n,
$$

o equivalentemente,

$$
C_{n+1}=(1-r)C_n.
$$

La solución es

$$
C_n=C_0(1-r)^n.
$$

Este modelo describe una disminución exponencial discreta.

Por ejemplo, si cada hora se elimina el $10%$ de una sustancia, entonces

$$
C_{n+1}=0.9C_n.
$$

Después de $n$ horas,

$$
C_n=C_0(0.9)^n.
$$

### 9.4 Física

Los modelos discretos también permiten aproximar sistemas físicos continuos.

Consideremos el movimiento de una partícula.

Si conocemos su posición $x_n$ y velocidad $v_n$ en el instante $n$, podemos aproximar

$$
x_{n+1}=x_n+v_n\Delta t,
$$

y

$$
v_{n+1}=v_n+a_n\Delta t,
$$

donde $a_n$ es la aceleración.

Estas ecuaciones constituyen un modelo discreto del movimiento.

Esta idea será fundamental cuando estudiemos métodos numéricos para ecuaciones diferenciales.

### 9.5 Ciencias ambientales

Consideremos un lago en el que una sustancia contaminante se elimina a una tasa proporcional a su concentración y, simultáneamente, existe una fuente externa constante $Q$.

Un modelo sencillo es

$$
C_{n+1}=(1-r)C_n+Q.
$$

El término

$$
-rC_n
$$

representa la eliminación de contaminante, mientras que $Q$ representa el aporte externo.

El equilibrio satisface

$$
C^*=(1-r)C^*+Q.
$$

Por tanto,

$$
rC^*=Q,
$$

y

$$
C^*=\frac{Q}{r}.
$$

Este ejemplo muestra cómo los puntos fijos pueden tener una interpretación científica directa.

Además, permite observar una idea importante: un equilibrio no significa necesariamente que todos los procesos del sistema se hayan detenido. En este caso, el contaminante continúa ingresando y eliminándose, pero ambos procesos se compensan exactamente en el equilibrio.

## 10. Modelos discretos acoplados

### 10.1 Más de una variable

Hasta ahora hemos estudiado sistemas descritos mediante una sola variable:

$$
x_{n+1}=f(x_n).
$$

Sin embargo, muchos fenómenos científicos requieren varias variables que evolucionan simultáneamente.

Por ejemplo,

$$
x_{n+1}=f(x_n,y_n),
$$

$$
y_{n+1}=g(x_n,y_n).
$$

En este caso decimos que tenemos un **modelo discreto acoplado**.

La característica fundamental es que las variables interactúan entre sí.

Podemos representar el estado del sistema mediante el vector

$$
\mathbf{x}_n=
\begin{pmatrix}
x_n\\
y_n
\end{pmatrix}.
$$

Entonces el modelo puede escribirse de manera compacta como

$$
\mathbf{x}_{n+1}
=
\mathbf{F}(\mathbf{x}_n).
$$

Esta notación será especialmente útil cuando estudiemos sistemas de mayor dimensión.

### 10.2 Modelo presa-depredador

Consideremos una población de presas $P_n$ y una población de depredadores $D_n$.

Un modelo sencillo puede ser

$$
P_{n+1}
=
P_n+rP_n-aP_nD_n,
$$

$$
D_{n+1}
=
D_n+bP_nD_n-dD_n.
$$

Los parámetros representan:

* $r$: tasa de crecimiento de las presas;
* $a$: intensidad de depredación;
* $b$: beneficio reproductivo de los depredadores debido a las presas;
* $d$: tasa de mortalidad de los depredadores.

El término

$$
aP_nD_n
$$

representa los encuentros entre presas y depredadores.

Por tanto, aparece con signo negativo en la ecuación de las presas:

$$
-aP_nD_n,
$$

y con signo positivo en la ecuación de los depredadores:

$$
+bP_nD_n.
$$

Este es un ejemplo de cómo una misma interacción puede afectar diferentes componentes del sistema.

### 10.3 Simulación del modelo

El modelo puede implementarse directamente:

```python
import numpy as np
import matplotlib.pyplot as plt

num_steps = 100

P = np.zeros(num_steps + 1)
D = np.zeros(num_steps + 1)

P[0] = 40
D[0] = 10

r = 0.1
a = 0.01
b = 0.005
d = 0.1

for n in range(num_steps):
    P[n + 1] = P[n] + r * P[n] - a * P[n] * D[n]
    D[n + 1] = D[n] + b * P[n] * D[n] - d * D[n]

plt.plot(P, label="Presas")
plt.plot(D, label="Depredadores")
plt.xlabel("Tiempo")
plt.ylabel("Población")
plt.legend()
plt.grid()
plt.show()
```

La simulación permite observar cómo la interacción entre las dos poblaciones puede generar oscilaciones.

Es importante, sin embargo, no interpretar automáticamente una gráfica como evidencia de que el fenómeno real se comporta exactamente de esa manera. La simulación muestra las consecuencias de **las hipótesis incorporadas en el modelo**. Si el modelo produce oscilaciones, debemos preguntarnos qué mecanismos del modelo son responsables de ellas y si esos mecanismos son razonables para el fenómeno estudiado.

### 10.4 Otros modelos acoplados

Los modelos acoplados aparecen en muchas áreas.

**Epidemiología:**

$$
S_{n+1}=f(S_n,I_n),
$$

$$
I_{n+1}=g(S_n,I_n).
$$

**Química:**

$$
C_{1,n+1}=f(C_{1,n},C_{2,n}),
$$

$$
C_{2,n+1}=g(C_{1,n},C_{2,n}).
$$

**Ecología:**

$$
N_{1,n+1}=f(N_{1,n},N_{2,n}),
$$

$$
N_{2,n+1}=g(N_{1,n},N_{2,n}).
$$

**Economía:**

$$
K_{n+1}=f(K_n,C_n),
$$

$$
C_{n+1}=g(K_n,C_n).
$$

En todos estos casos, la evolución de una variable depende de las demás.

La idea de acoplamiento es fundamental: el comportamiento del sistema completo no puede entenderse necesariamente estudiando cada variable de manera independiente.

## 11. Análisis cualitativo de un modelo discreto

Una simulación numérica produce valores, pero el objetivo del modelamiento matemático es comprender el comportamiento del sistema.

Para un modelo

$$
x_{n+1}=f(x_n),
$$

podemos formular preguntas como:

1. ¿Cuáles son los puntos fijos?
2. ¿Son estables?
3. ¿La solución crece o decrece?
4. ¿La sucesión converge?
5. ¿Existen oscilaciones?
6. ¿El comportamiento depende de la condición inicial?
7. ¿Cómo cambia la dinámica cuando modificamos los parámetros?
8. ¿El modelo es razonable para el fenómeno estudiado?

Estas preguntas permiten pasar de una simple simulación a un verdadero análisis matemático.

### 11.1 El papel de los parámetros

Los parámetros de un modelo representan propiedades del fenómeno.

Por ejemplo, en

$$
N_{n+1}
=
N_n+rN_n
\left(1-\frac{N_n}{K}\right),
$$

$r$ puede representar una tasa de crecimiento, mientras que $K$ representa una capacidad de carga.

Modificar los parámetros equivale a modificar las hipótesis sobre el sistema.

Por ello, una parte esencial del modelamiento consiste en estudiar la **sensibilidad del modelo respecto de sus parámetros**.

Una pregunta típica es:

> ¿Qué cambios en el comportamiento del sistema producen pequeñas variaciones en los parámetros?

Por ejemplo, si un modelo poblacional predice que una población converge a $K$, podemos investigar qué ocurre cuando $K$ cambia o cuando la tasa $r$ aumenta.

### 11.2 Condiciones iniciales

El estado inicial también puede afectar la evolución.

Dos sistemas con la misma regla

$$
x_{n+1}=f(x_n)
$$

pero con diferentes condiciones iniciales

$$
x_0=x_{\mathrm{ini}}^{(1)}
$$

y

$$
x_0=x_{\mathrm{ini}}^{(2)}
$$

pueden generar trayectorias diferentes.

Por esta razón, una simulación completa debe especificar tanto el modelo como las condiciones iniciales.

En algunos sistemas, las diferencias entre condiciones iniciales desaparecen con el tiempo porque las trayectorias convergen hacia el mismo equilibrio. En otros, pequeñas diferencias iniciales pueden producir comportamientos significativamente diferentes.

Esta sensibilidad respecto de las condiciones iniciales será especialmente importante al estudiar sistemas dinámicos no lineales.

### 11.3 Un ejemplo de análisis completo

Consideremos nuevamente

$$
x_{n+1}=\frac12x_n+2.
$$

Podemos analizar el modelo siguiendo una secuencia lógica.

**Paso 1. Encontrar los puntos fijos.**

Resolvemos

$$
x^*=\frac12x^*+2,
$$

obteniendo

$$
x^*=4.
$$

**Paso 2. Estudiar la estabilidad.**

Como

$$
f'(x)=\frac12,
$$

tenemos

$$
|f'(4)|=\frac12<1.
$$

Por tanto, el equilibrio es localmente estable.

**Paso 3. Observar una trayectoria.**

Si

$$
x_0=10,
$$

entonces

$$
x_1=7,
$$

$$
x_2=5.5,
$$

$$
x_3=4.75,
$$

$$
x_4=4.375.
$$

La trayectoria se aproxima a $4$.

**Paso 4. Interpretar.**

El modelo predice que, independientemente de una perturbación moderada del estado inicial, el sistema retorna progresivamente hacia el nivel de equilibrio $x^*=4$.

Este procedimiento constituye un ejemplo sencillo de cómo combinar cálculo, análisis cualitativo y simulación.

## 12. Ideas principales

Los conceptos fundamentales de este capítulo pueden resumirse de la siguiente manera.

### Sucesiones

Una sucesión

$$
\{x_n\}_{n=0}^{\infty}
$$

puede representar la evolución de un sistema en tiempos discretos.

### Recurrencias

Una regla de evolución puede escribirse como

$$
x_{n+1}=f(x_n).
$$

### Ecuaciones en diferencias

El cambio discreto entre dos estados consecutivos es

$$
x_{n+1}-x_n.
$$

Cuando el intervalo temporal es $\Delta t$, la tasa de cambio discreta es

$$
\frac{x_{n+1}-x_n}{\Delta t}.
$$

### Punto fijo

Un equilibrio satisface

$$
f(x^*)=x^*.
$$

### Estabilidad

Para un punto fijo diferenciable, el criterio local fundamental es

$$
|f'(x^*)|<1
$$

para estabilidad local, mientras que

$$
|f'(x^*)|>1
$$

indica inestabilidad local.

### Modelos poblacionales

El crecimiento exponencial discreto tiene la forma

$$
x_{n+1}=(1+r)x_n,
$$

mientras que un modelo logístico discreto sencillo puede escribirse como

$$
N_{n+1}
=
N_n+rN_n
\left(1-\frac{N_n}{K}\right).
$$

### Sistemas acoplados

Cuando varias variables interactúan,

$$
x_{n+1}=f(x_n,y_n),
$$

$$
y_{n+1}=g(x_n,y_n).
$$

De manera compacta,

$$
\mathbf{x}_{n+1}
=
\mathbf{F}(\mathbf{x}_n).
$$

### Modelamiento computacional

Una ecuación recurrente puede convertirse directamente en un algoritmo iterativo:

$$
\text{modelo}
\rightarrow
\text{algoritmo}
\rightarrow
\text{simulación}.
$$

Pero una simulación no sustituye al análisis matemático. El objetivo es comprender qué consecuencias tienen las hipótesis del modelo y determinar si esas consecuencias son razonables para el fenómeno estudiado.

## 13. Ejercicios

### Ejercicio 1. Sucesiones

Considere la sucesión

$$
x_n=3n+2.
$$

1. Calcule los primeros cinco términos.
2. Determine si la sucesión es creciente o decreciente.
3. ¿La sucesión converge?
4. Determine una expresión para $x_{100}$.

### Ejercicio 2. Sucesión recurrente

Considere

$$
x_{n+1}=0.8x_n+1,
$$

con

$$
x_0=0.
$$

1. Calcule los primeros diez términos.
2. Determine el punto fijo.
3. Analice la estabilidad del punto fijo.
4. Conjeture el comportamiento de la sucesión cuando $n\to\infty$.
5. Compare la conjetura con una simulación numérica.

### Ejercicio 3. Crecimiento poblacional

Una población de bacterias contiene inicialmente $500$ individuos y aumenta un $15%$ cada hora.

1. Construya una ecuación recurrente para la población.
2. Calcule la población después de $10$ horas.
3. Obtenga una fórmula explícita para $N_n$.
4. Grafique la población durante las primeras $20$ horas.
5. ¿Qué limitación tendría este modelo si se utilizara durante un periodo de tiempo muy largo?

### Ejercicio 4. Decaimiento

Una sustancia pierde el $8%$ de su concentración cada hora. Inicialmente,

$$
C_0=100.
$$

1. Construya el modelo discreto.
2. Determine una expresión explícita para $C_n$.
3. Calcule la concentración después de $12$ horas.
4. Determine aproximadamente después de cuántas horas la concentración será menor que $20$.
5. Interprete el resultado en términos del fenómeno físico o químico.

### Ejercicio 5. Punto fijo

Considere el modelo

$$
x_{n+1}=0.3x_n+7.
$$

1. Determine el punto fijo.
2. Analice su estabilidad.
3. Simule el modelo para $x_0=0$.
4. Compare la simulación con el valor del punto fijo.
5. Repita la simulación utilizando $x_0=20$ y compare las dos trayectorias.

### Ejercicio 6. Modelo logístico

Considere

$$
N_{n+1}
=
N_n+0.2N_n
\left(1-\frac{N_n}{500}\right),
$$

con

$$
N_0=20.
$$

1. Calcule los primeros diez términos.
2. Determine los puntos fijos.
3. Analice la estabilidad local de cada punto fijo.
4. Simule el modelo durante $100$ pasos.
5. Grafique la población.
6. ¿Hacia qué valor parece converger?
7. Compare el comportamiento con el modelo exponencial correspondiente.

### Ejercicio 7. Efecto de los parámetros

Considere nuevamente el modelo logístico

$$
N_{n+1}
=
N_n+rN_n
\left(1-\frac{N_n}{K}\right).
$$

Realice simulaciones modificando los valores de $r$ y manteniendo fijo $K$.

1. ¿Qué sucede cuando $r$ es pequeño?
2. ¿Qué sucede cuando $r$ aumenta?
3. ¿Se observan oscilaciones?
4. ¿Cómo cambia el comportamiento cualitativo del sistema?
5. ¿Qué relación observa entre el valor del parámetro $r$ y la estabilidad de los equilibrios?

### Ejercicio 8. Contaminación

La concentración de un contaminante en un lago satisface

$$
C_{n+1}=(1-r)C_n+Q.
$$

Suponga

$$
r=0.1,
\qquad
Q=5,
\qquad
C_0=20.
$$

1. Calcule los primeros diez valores.
2. Determine el punto fijo.
3. Analice su estabilidad.
4. Interprete físicamente el punto fijo.
5. ¿Qué ocurre si se duplica el aporte externo $Q$?
6. ¿Qué sucede con el equilibrio si aumenta la tasa de eliminación $r$?

### Ejercicio 9. Presa-depredador

Considere el modelo

$$
P_{n+1}
=
P_n+rP_n-aP_nD_n,
$$

$$
D_{n+1}
=
D_n+bP_nD_n-dD_n.
$$

Use los valores

$$
P_0=40,
\qquad
D_0=10,
$$

$$
r=0.1,
\qquad
a=0.01,
\qquad
b=0.005,
\qquad
d=0.1.
$$

1. Implemente el modelo en Python.
2. Simule durante $100$ pasos.
3. Grafique ambas poblaciones.
4. Describa el comportamiento observado.
5. ¿Qué ocurre si aumenta la tasa de mortalidad $d$?
6. Investigue qué sucede si se modifica la intensidad de depredación $a$.

### Ejercicio 10. Modelamiento de un fenómeno científico

Seleccione un fenómeno de interés en alguna de las siguientes áreas:

* biología;
* ecología;
* química;
* física;
* ciencias ambientales;
* economía.

Construya un modelo de cambio discreto siguiendo las siguientes etapas:

1. describa el fenómeno;
2. identifique las variables relevantes;
3. establezca las hipótesis;
4. defina las variables y parámetros;
5. construya una regla de evolución;
6. especifique las condiciones iniciales;
7. implemente el modelo en Python;
8. grafique los resultados;
9. analice el comportamiento;
10. interprete los resultados en términos del fenómeno original.

El objetivo no es solamente obtener una simulación, sino explicar cómo las hipótesis sobre el fenómeno conducen al modelo matemático y cómo el modelo permite obtener conclusiones sobre el sistema.

Como parte del análisis, discuta también al menos una **limitación del modelo** y proponga una posible modificación que permita representar mejor el fenómeno.

## 14. Hacia los modelos continuos

En este capítulo hemos descrito sistemas mediante estados discretos

$$
x_0,x_1,x_2,\ldots
$$

y reglas de evolución como

$$
x_{n+1}=f(x_n).
$$

Esta descripción es apropiada cuando observamos el sistema en intervalos separados de tiempo.

Sin embargo, muchos fenómenos físicos, químicos y biológicos evolucionan de manera continua. En estos casos podemos representar el estado mediante una función

$$
x=x(t),
$$

donde $t$ es una variable continua.

El cambio discreto

$$
\frac{x_{n+1}-x_n}{\Delta t}
$$

se convierte, en el límite cuando

$$
\Delta t\rightarrow0,
$$

en la derivada

$$
\frac{dx}{dt}.
$$

Por ejemplo, consideremos el modelo discreto

$$
x_{n+1}=x_n+r x_n\Delta t.
$$

Podemos escribirlo como

$$
\frac{x_{n+1}-x_n}{\Delta t}=rx_n.
$$

Cuando el intervalo $\Delta t$ se hace cada vez más pequeño, esta expresión conduce formalmente a

$$
\frac{dx}{dt}=rx.
$$

Así, el modelo continuo correspondiente describe un crecimiento proporcional mediante una ecuación diferencial.

Esta conexión muestra que los modelos discretos y continuos no son mundos completamente separados. Las ecuaciones en diferencias pueden utilizarse para construir aproximaciones de modelos continuos y, a su vez, ciertos modelos discretos pueden interpretarse como versiones de tiempo discreto de modelos continuos.

Así aparece una nueva clase de modelos:

$$
\boxed{
\text{modelos discretos}
\quad\longrightarrow\quad
\text{modelos continuos}
}
$$

Esta transición nos llevará al estudio de las **ecuaciones diferenciales**, que constituyen una de las herramientas fundamentales para describir fenómenos que evolucionan continuamente en el tiempo.
