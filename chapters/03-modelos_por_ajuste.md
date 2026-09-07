# Modelos por ajuste a datos

En muchos problemas de modelamiento matemático conocemos un fenómeno, realizamos observaciones o disponemos de datos experimentales, pero no conocemos de antemano la relación matemática que existe entre las variables involucradas.

Por ejemplo, podemos observar cómo cambia la longitud de un resorte cuando aplicamos diferentes fuerzas, cómo varía la presión de un gas con su volumen, cómo crece una población bacteriana o cómo cambia la concentración de una sustancia con el tiempo.

En todos estos casos, los datos pueden utilizarse para construir un modelo matemático que permita describir el comportamiento observado y, eventualmente, realizar predicciones.

Una de las herramientas fundamentales para este propósito es la **regresión**. En particular, la **regresión lineal por mínimos cuadrados** constituye una de las herramientas más importantes para construir modelos a partir de datos.

La importancia de la regresión lineal va mucho más allá de encontrar una recta. Muchas funciones que aparentemente no son lineales pueden transformarse de manera que sus parámetros puedan determinarse mediante una regresión lineal. Además, la misma idea de minimizar errores conduce a métodos de ajuste mucho más generales.

<br><br>

## 1. La regresión lineal como herramienta para construir modelos

Supongamos que tenemos un conjunto de datos

$$
(x_1,y_1),\,(x_2,y_2),\,\ldots,\,(x_n,y_n),
$$

donde $x$ representa una variable independiente y $y$ una variable dependiente.

Una primera pregunta que podemos hacernos es:

> ¿Existe una relación matemática sencilla que permita describir cómo depende $y$ de $x$?

Una posibilidad es buscar una relación lineal de la forma

$$
y=mx+b.
$$

En general, los puntos experimentales no se encuentran exactamente sobre una misma recta. Por esta razón, no buscamos una recta que pase por todos los puntos, sino una recta que represente de la mejor manera posible la tendencia de los datos.

Este problema conduce al método de **mínimos cuadrados**.

La regresión lineal es especialmente importante porque constituye una pieza fundamental para construir muchos otros modelos. Por ejemplo:

- modelos lineales;
- modelos polinomiales;
- modelos exponenciales;
- modelos de potencia;
- modelos linealizables mediante transformaciones;
- modelos construidos por tramos.

Por esta razón, en este capítulo la regresión lineal será considerada como una de las herramientas centrales para la construcción de modelos basados en datos.

<br><br>

## 2. Regresión lineal por mínimos cuadrados

### 2.1 El modelo lineal

Consideremos un conjunto de datos

$$
\mathcal{D}=
\{(x_i,y_i):i=1,\ldots,n\}.
$$

Queremos encontrar una función lineal

$$
f(x)=mx+b
$$

que represente razonablemente los datos.

Aquí:

- $m$ es la **pendiente** de la recta;
- $b$ es la **intersección con el eje $y$**.

Si el modelo es adecuado, para cada valor $x_i$ esperamos que

$$
f(x_i)\approx y_i.
$$

Denotaremos por

$$
\widehat{y}_i=f(x_i)=mx_i+b
$$

el valor predicho por el modelo.

La diferencia entre el valor observado y el valor predicho se denomina **residuo**:

$$
r_i=y_i-\widehat{y}_i.
$$

Por tanto,

$$
r_i=y_i-(mx_i+b).
$$

<br>

### 2.2 El criterio de mínimos cuadrados

Una forma natural de medir qué tan bien se ajusta una recta a los datos consiste en sumar los cuadrados de los residuos:

$$
E(m,b) =
\sum_{i=1}^{n} ( y_i-(mx_i+b) )^2.
$$

La función $E(m,b)$ se denomina **función de error** o **suma de cuadrados de los residuos**.

El método de mínimos cuadrados consiste en encontrar los valores de $m$ y $b$ que minimizan esta cantidad:

$$
\boxed{
(m,b)=
\operatorname*{arg\,min}_{(m,b)} E(m,b)
}
$$

La recta obtenida de esta manera se denomina **recta de regresión**.

<br>

### 2.3 Interpretación geométrica

La recta de regresión no tiene por qué pasar exactamente por los puntos experimentales.

Para cada punto $(x_i,y_i)$, el modelo produce un valor

$$
\widehat{y}_i=mx_i+b.
$$

El residuo

$$
r_i=y_i-\widehat{y}_i
$$

representa la diferencia vertical entre el dato observado y el valor predicho por la recta.

El método de mínimos cuadrados busca la recta que minimiza

$$
r_1^2+r_2^2+\cdots+r_n^2.
$$

Por tanto, los residuos positivos y negativos no se cancelan entre sí.

<br>

### 2.4 Una observación importante

El criterio de mínimos cuadrados penaliza los errores grandes más fuertemente que los errores pequeños.

Por ejemplo,

$$
1^2=1,
\qquad
2^2=4,
\qquad
5^2=25.
$$

Un error cinco veces mayor contribuye veinticinco veces más a la función de error.

Esta propiedad hace que el método sea particularmente útil cuando queremos encontrar un modelo que represente globalmente la tendencia de los datos.

<br><br>

## 3. Teorema de regresión lineal por mínimos cuadrados

### Teorema

Sean

$$
(x_1,y_1),\ldots,(x_n,y_n)
$$

un conjunto de datos, y supongamos que los valores $x_i$ no son todos iguales.

Entonces existe una única recta

$$
f(x)=mx+b
$$

que minimiza

$$
E(m,b) =
\sum_{i=1}^{n}
\left[y_i-(mx_i+b)\right]^2.
$$

Los parámetros $m$ y $b$ están dados por

$$
\boxed{
m=
\frac{
\displaystyle
\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})
}{
\displaystyle
\sum_{i=1}^{n}(x_i-\bar{x})^2
}
}
$$

y

$$
\boxed{
b=\bar{y}-m\bar{x}
}
$$

donde

$$
\bar{x} = \frac{1}{n} \sum_{i=1}^{n}x_i,
\qquad \bar{y} =
\frac{1}{n}
\sum_{i=1}^{n}y_i.
$$

<br>

### Demostración

Partimos de

$$
E(m,b) =
\sum_{i=1}^{n}
[y_i-(mx_i+b)]^2.
$$

Para minimizar $E$, buscamos un punto crítico:

$$
\frac{\partial E}{\partial m}=0,
\qquad
\frac{\partial E}{\partial b}=0.
$$

Calculamos primero la derivada respecto a $m$:

$$
\frac{\partial E}{\partial m} =
-2
\sum_{i=1}^{n}
x_i[y_i-(mx_i+b)].
$$

Por tanto,

$$
\sum_{i=1}^{n}
x_i[y_i-(mx_i+b)]
=0.
$$

Desarrollando,

$$
\sum_{i=1}^{n}x_i y_i -
m\sum_{i=1}^{n}x_i^2 -
b\sum_{i=1}^{n}x_i
=0.
$$

De manera equivalente,

$$
m\sum_{i=1}^{n}x_i^2
+
b\sum_{i=1}^{n}x_i =
\sum_{i=1}^{n}x_i y_i.
$$

Ahora derivamos respecto a $b$:

$$
\frac{\partial E}{\partial b}=
-2
\sum_{i=1}^{n}
[y_i-(mx_i+b)].
$$

Por tanto,

$$
\sum_{i=1}^{n}
[y_i-(mx_i+b)]
=0.
$$

De donde

$$
\sum_{i=1}^{n}y_i -
m\sum_{i=1}^{n}x_i -
nb
=0.
$$

Así,

$$
m\sum_{i=1}^{n}x_i+nb =
\sum_{i=1}^{n}y_i.
$$

Dividiendo entre $n$,

$$
m\bar{x}+b=\bar{y}.
$$

Por tanto,

$$
\boxed{
b=\bar{y}-m\bar{x}.
}
$$

Sustituyendo esta expresión en la primera ecuación y reorganizando se obtiene

$$
\boxed{
m=
\frac{
\sum_{i=1}^{n}(x_i-\bar{x})(y_i-\bar{y})
}{
\sum_{i=1}^{n}(x_i-\bar{x})^2
}.
}
$$

Finalmente,

$$
\boxed{
b=\bar{y}-m\bar{x}.
}
$$

Estas expresiones proporcionan los parámetros de la recta de mínimos cuadrados.

<br><br>

## 4. Interpretación de los parámetros

Una vez obtenida la recta

$$
f(x)=mx+b,
$$

sus parámetros deben interpretarse en el contexto del problema.

### 4.1 La pendiente

La pendiente $m$ mide el cambio promedio de $y$ asociado a un cambio unitario en $x$.

Si

$$
m>0,
$$

el modelo indica una tendencia creciente.

Si

$$
m<0,
$$

el modelo indica una tendencia decreciente.

Si

$$
m\approx0,
$$

el modelo lineal indica que no existe una tendencia lineal marcada.

Las unidades de $m$ son

$$
\frac{\text{unidades de }y}
{\text{unidades de }x}.
$$

<br>

### 4.2 El intercepto

El parámetro $b$ corresponde al valor que predice el modelo cuando

$$
x=0.
$$

Sin embargo, esto no significa necesariamente que $b$ tenga una interpretación física relevante.

Por ejemplo, si nuestros datos corresponden a temperaturas entre $20^\circ C$ y $40^\circ C$, el valor $x=0$ puede estar fuera del rango de interés.

Por esta razón, los parámetros de un modelo siempre deben interpretarse dentro del contexto del problema.

<br><br>

## 5. Evaluación del ajuste: residuos y $R^2$

Encontrar una recta de mínimos cuadrados no garantiza que esta sea un buen modelo.

Es necesario evaluar qué tan bien representa los datos.

Una herramienta fundamental son los residuos:

$$
r_i=y_i-\widehat{y}_i.
$$

Si los residuos son pequeños, el modelo reproduce razonablemente los datos.

Pero no solamente importa su magnitud. También debemos estudiar su comportamiento.

Si los residuos muestran patrones sistemáticos, puede indicar que una recta no es un modelo adecuado.

Por ejemplo, si los residuos presentan una estructura curva, puede ser necesario utilizar un modelo no lineal.

<br>

### 5.1 El coeficiente de determinación

Una medida frecuente del ajuste lineal es el coeficiente de determinación

$$
R^2.
$$

Se define como

$$
R^2 =
1-
\frac{
\displaystyle\sum_{i=1}^{n}(y_i-\widehat{y}_i)^2
}{
\displaystyle\sum_{i=1}^{n}(y_i-\bar{y})^2
}.
$$

El numerador mide la variabilidad que queda sin explicar por el modelo, mientras que el denominador representa la variabilidad total de los datos.

Un valor de $R^2$ cercano a $1$ indica que el modelo explica una gran parte de la variabilidad observada.

Sin embargo, un valor alto de $R^2$ **no demuestra por sí mismo que el modelo sea correcto**.

Un buen modelo debe analizarse también desde el punto de vista matemático y del fenómeno que representa.

<br><br>

## 6. La regresión lineal como corazón de otros modelos

La importancia de la regresión lineal no se limita al modelo

$$
y=mx+b.
$$

La misma idea puede utilizarse para construir modelos cuya expresión final no es una recta.

La clave está en reconocer que una expresión puede ser no lineal respecto a las variables, pero **lineal respecto a sus parámetros**.

<br>

### 6.1 Modelos polinomiales

Consideremos el modelo cuadrático

$$
y=ax^2+bx+c.
$$

Este modelo no es una función lineal de $x$. Sin embargo, es lineal respecto a los parámetros $a,b,c$.

Podemos escribirlo como

$$
y =
a\,x^2+b\,x+c.
$$

Definamos

$$
X_1=x^2,
\qquad
X_2=x,
\qquad
X_3=1.
$$

Entonces

$$
y=aX_1+bX_2+cX_3.
$$

El problema puede resolverse utilizando mínimos cuadrados.

De manera general, un modelo polinomial de grado $k$ tiene la forma

$$
y=a_0+a_1x+a_2x^2+\cdots+a_kx^k.
$$

Aunque la función no sea lineal en $x$, el modelo es lineal en los parámetros

$$
a_0,a_1,\ldots,a_k.
$$

Por esta razón, los modelos polinomiales pueden construirse mediante una generalización de la regresión lineal.

<br>

### 6.2 Modelos exponenciales

Supongamos que proponemos el modelo

$$
y=Ae^{Bx}.
$$

Este modelo no es lineal en $x$. Sin embargo, podemos aplicar logaritmo natural:

$$
\ln y=\ln A+Bx.
$$

Definiendo

$$
Y=\ln y,
\qquad
a=\ln A,
$$

obtenemos

$$
Y=a+Bx.
$$

Ahora tenemos un modelo lineal.

Podemos realizar una regresión lineal entre $x$ y $\ln y$, obtener $a$ y $B$, y luego recuperar

$$
A=e^a.
$$

Por tanto,

$$
\boxed{
y=Ae^{Bx}
}
$$

puede construirse a partir de una regresión lineal después de una transformación apropiada.

<br>

### 6.3 Modelos de potencia

Consideremos ahora

$$
y=Ax^B.
$$

Aplicando logaritmo,

$$
\ln y=\ln A+B\ln x.
$$

Definiendo

$$
Y=\ln y,
\qquad
X=\ln x,
\qquad
a=\ln A,
$$

obtenemos

$$
Y=a+BX.
$$

Nuevamente aparece una regresión lineal.

Después de determinar $a$ y $B$, recuperamos

$$
A=e^a.
$$

Así,

$$
\boxed{
y=Ax^B
}
$$

puede construirse mediante una transformación logarítmica y una regresión lineal.

<br>

### 6.4 Una idea fundamental

Estos ejemplos muestran una idea central:

> La regresión lineal no debe entenderse únicamente como el ajuste de una recta. Es una herramienta fundamental para determinar parámetros de modelos matemáticos a partir de datos.

La pregunta importante no es solamente:

> ¿Qué recta se ajusta a los datos?

sino también:

> ¿Qué transformación o formulación del problema permite utilizar las herramientas de regresión para construir un modelo adecuado?

Esta perspectiva será importante en los capítulos posteriores.

<br><br>

## 7. Ejemplo: ajuste de un modelo a datos experimentales

Supongamos que se estudia la relación entre la concentración de un nutriente y el crecimiento de una población bacteriana.

Se obtienen los siguientes datos:

| Concentración $x$ (mg/L) | Población $y$ |
|---:|---:|
| 1 | 20000 |
| 2 | 25000 |
| 3 | 35000 |
| 4 | 40000 |
| 5 | 45000 |
| 6 | 50000 |

Queremos construir un modelo lineal

$$
y=mx+b.
$$

Podemos utilizar Python para realizar el cálculo.

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.array([1, 2, 3, 4, 5, 6])
y = np.array([20000, 25000, 35000, 40000, 45000, 50000])

m, b = np.polyfit(x, y, 1)

print("Pendiente:", m)
print("Intercepto:", b)
```

El resultado es aproximadamente

$$
m\approx6142.86,
$$

y

$$
b\approx14333.33.
$$

Por tanto, el modelo es

$$
\boxed{
y\approx6142.86x+14333.33.
}
$$

Podemos visualizar los datos junto con el modelo:

```python
y_modelo = m*x + b

plt.scatter(x, y, label="Datos")
plt.plot(x, y_modelo, label="Regresión lineal")

plt.xlabel("Concentración (mg/L)")
plt.ylabel("Población")
plt.legend()
plt.show()
```

El modelo permite realizar predicciones dentro del rango observado.

Por ejemplo, para una concentración de $x=4.5$ mg/L:

```python
x_nuevo = 4.5
y_pred = m*x_nuevo + b

print(y_pred)
```

obtenemos aproximadamente

$$
y(4.5)\approx41976.19.
$$

Es importante observar que esta predicción se encuentra **dentro del intervalo de valores utilizados para construir el modelo**.

Esto nos conduce a distinguir entre interpolación y extrapolación.

<br><br>

## 8. Cuando una sola función no describe adecuadamente los datos

En algunos problemas, una única función sencilla puede ser insuficiente para describir todo el conjunto de datos.

Por ejemplo, consideremos los datos

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

Los datos primero aumentan y posteriormente disminuyen.

Una única recta no puede representar adecuadamente este comportamiento.

Además, si interpretamos $y$ como función de $x$, la relación es una función, pero no es inyectiva: por ejemplo,

$$
f(4)=f(6)=14.
$$

Esto significa que dos valores diferentes de $x$ pueden producir el mismo valor de $y$.

Sin embargo, **la falta de inyectividad no impide que podamos construir un modelo $y=f(x)$**.

El problema real es que la relación cambia de comportamiento en diferentes regiones del dominio.

Una estrategia natural consiste en dividir los datos en dos regiones.

<br>

### 8.1 Primer tramo

Para

$$
0\leq x\leq5
$$

ajustamos una recta

$$
f_1(x)=m_1x+b_1.
$$

Aplicando mínimos cuadrados obtenemos aproximadamente

$$
m_1=2.7143,
\qquad
b_1=2.3810.
$$

Por tanto,

$$
\boxed{
f_1(x)=2.7143x+2.3810.
}
$$

<br>

### 8.2 Segundo tramo

Para

$$
5\leq x\leq10
$$

ajustamos una segunda recta

$$
f_2(x)=m_2x+b_2.
$$

El ajuste produce

$$
m_2=-2.7143,
\qquad
b_2=29.5238.
$$

Por tanto,

$$
\boxed{
f_2(x)=-2.7143x+29.5238.
}
$$

<br>

### 8.3 Modelo por tramos

Podemos combinar ambos modelos en una única función:

$$
\boxed{
f(x)=
\begin{cases}
2.7143x+2.3810,
&0\leq x\leq5,\\[4pt]
-2.7143x+29.5238,
&5<x\leq10.
\end{cases}
}
$$

Hemos construido así un **modelo por tramos**.

La idea general es muy importante:

> Cuando diferentes regiones de los datos presentan comportamientos diferentes, puede ser más adecuado construir varios modelos locales y combinarlos en una función por tramos.

En este ejemplo, las dos rectas incluso coinciden en el punto de transición $x=5$. Esto ocurre debido a la simetría de los datos; en general, dos ajustes independientes no tienen por qué coincidir exactamente en el punto donde se separan los datos.

<br>

### 8.4 Implementación en Python

El procedimiento puede implementarse directamente:

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.arange(0, 11)
y = np.array([2, 5, 8, 11, 14, 15, 14, 11, 8, 5, 2])

# Primer tramo
x1 = x[x <= 5]
y1 = y[x <= 5]

m1, b1 = np.polyfit(x1, y1, 1)

# Segundo tramo
x2 = x[x >= 5]
y2 = y[x >= 5]

m2, b2 = np.polyfit(x2, y2, 1)

print("Primer tramo:")
print("m1 =", m1)
print("b1 =", b1)

print("Segundo tramo:")
print("m2 =", m2)
print("b2 =", b2)
```

Podemos visualizar el resultado:

```python
x_plot = np.linspace(0, 10, 200)

y_plot = np.where(
    x_plot <= 5,
    m1*x_plot + b1,
    m2*x_plot + b2
)

plt.scatter(x, y, label="Datos")
plt.plot(x_plot, y_plot, label="Modelo por tramos")

plt.xlabel("x")
plt.ylabel("y")
plt.legend()
plt.show()
```

Este procedimiento puede generalizarse a modelos con más de dos regiones y también a modelos diferentes en cada tramo.

<br><br>

## 9. Interpolación

La **interpolación** es otra estrategia para construir información a partir de datos conocidos.

Supongamos que conocemos los valores

$$
(x_1,y_1),\ldots,(x_n,y_n).
$$

Queremos estimar el valor de $y$ para un punto $x^\ast$ que se encuentra **dentro del intervalo cubierto por los datos**.

Es decir, si

$$
x_{\min}\leq x^\ast\leq x_{\max},
$$

buscamos una estimación de

$$
y^\ast=f(x^\ast).
$$

La idea fundamental de la interpolación es construir una función que reproduzca exactamente los valores conocidos y utilizarla para estimar valores intermedios.

<br>

### 9.1 Interpolación frente a regresión

Es importante distinguir dos problemas diferentes.

En una regresión buscamos una función que represente la tendencia general de los datos minimizando algún criterio de error.

Por tanto, normalmente

$$
f(x_i)\neq y_i.
$$

En una interpolación, en cambio, construimos una función que satisface exactamente

$$
f(x_i)=y_i
$$

para todos los puntos conocidos.

Podemos resumir la diferencia de la siguiente manera:

| Regresión | Interpolación |
|---|---|
| Busca un modelo que represente la tendencia | Construye una función que pasa por los datos |
| Generalmente no pasa por todos los puntos | Pasa exactamente por los puntos dados |
| Tolera errores o ruido experimental | Reproduce exactamente los datos |
| Es útil para estimar tendencias | Es útil para estimar valores intermedios |
| Puede utilizar muchos puntos para encontrar un modelo global | Puede construir una función que pase por los puntos conocidos |

Esta diferencia es fundamental en el modelamiento matemático.

<br><br>

## 10. Interpolación lineal

La forma más sencilla de interpolación consiste en utilizar una recta entre dos puntos.

Supongamos que conocemos

$$
(x_1,y_1)
$$

y

$$
(x_2,y_2).
$$

La recta que pasa por ambos puntos es

$$
f(x)
=
y_1+
\frac{y_2-y_1}{x_2-x_1}(x-x_1).
$$

Si $x$ se encuentra entre $x_1$ y $x_2$, esta expresión proporciona una estimación interpolada.

<br>

### Ejemplo

Supongamos que sabemos que

$$
f(2)=5,
\qquad
f(6)=13.
$$

Queremos estimar $f(4)$.

La interpolación lineal produce

$$
f(4)
=
5+
\frac{13-5}{6-2}(4-2).
$$

Por tanto,

$$
f(4)=5+\frac{8}{4}(2)=9.
$$

Así,

$$
\boxed{f(4)\approx9.}
$$

En este caso, la interpolación lineal consiste simplemente en unir los dos puntos mediante una recta.

<br><br>

## 11. Interpolación polinomial

Podemos utilizar más de dos puntos para construir un polinomio que pase exactamente por todos ellos.

Supongamos que tenemos $n$ puntos con coordenadas $x_i$ diferentes.

Existe un polinomio de grado menor o igual que $n-1$,

$$
p(x),
$$

tal que

$$
p(x_i)=y_i,
\qquad
i=1,\ldots,n.
$$

Este polinomio se denomina **polinomio interpolante**.

Por ejemplo, con tres puntos podemos construir un polinomio cuadrático:

$$
p(x)=ax^2+bx+c.
$$

Los coeficientes $a,b,c$ se determinan imponiendo las tres condiciones

$$
p(x_1)=y_1,
$$

$$
p(x_2)=y_2,
$$

$$
p(x_3)=y_3.
$$

<br><br>

## 12. Interpolación de Lagrange

Una forma particularmente elegante de construir el polinomio interpolante es mediante la **interpolación de Lagrange**.

Sean

$$
(x_1,y_1),\ldots,(x_n,y_n)
$$

puntos con valores $x_i$ diferentes.

Definimos los polinomios de Lagrange

$$L_i(x)=
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

Por esta razón, el polinomio interpolante puede escribirse como

$$
\boxed{
p(x)=
\sum_{i=1}^{n}
y_iL_i(x)
}
$$

o, explícitamente,

$$
\boxed{
p(x)=
\sum_{i=1}^{n}
y_i
\prod_{\substack{j=1\\j\neq i}}^n
\frac{x-x_j}{x_i-x_j}.
}
$$

Esta expresión permite construir directamente un polinomio que pasa exactamente por todos los puntos.

<br>

### 12.1 Ejemplo de interpolación de Lagrange

Consideremos los puntos

$$
(0,1),\qquad(1,3),\qquad(2,2).
$$

Tenemos

$$
L_1(x) =
\frac{(x-1)(x-2)}
{(0-1)(0-2)} =
\frac{(x-1)(x-2)}{2},
$$

$$
L_2(x) =
\frac{(x-0)(x-2)}
{(1-0)(1-2)} =
-x(x-2),
$$

y

$$
L_3(x) =
\frac{(x-0)(x-1)}
{(2-0)(2-1)} =
\frac{x(x-1)}{2}.
$$

Por tanto,

$$
p(x) =
1L_1(x)+3L_2(x)+2L_3(x).
$$

Al simplificar,

$$
\boxed{
p(x) =
-\frac{3}{2}x^2
+\frac{7}{2}x
+1.
}
$$

Podemos verificar que

$$
p(0)=1,
\qquad
p(1)=3,
\qquad
p(2)=2.
$$

Por construcción, el polinomio pasa exactamente por los tres puntos.

<br>

### 12.2 Interpolación de Lagrange en Python

Podemos construir el polinomio utilizando `numpy`:

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.array([0, 1, 2])
y = np.array([1, 3, 2])

coeficientes = np.polyfit(x, y, 2)

p = np.poly1d(coeficientes)

x_plot = np.linspace(0, 2, 200)
y_plot = p(x_plot)

plt.scatter(x, y, label="Datos")
plt.plot(x_plot, y_plot, label="Polinomio interpolante")

plt.xlabel("x")
plt.ylabel("y")
plt.legend()
plt.show()
```

En este caso, `numpy` permite obtener el mismo polinomio que hemos construido matemáticamente.

<br><br>

## 13. Interpolación, regresión y extrapolación

Estas tres ideas están relacionadas, pero corresponden a problemas diferentes.

### 13.1 Interpolación

La interpolación consiste en estimar valores **dentro del rango de los datos conocidos**.

Si nuestros datos cubren

$$
x_{\min}\leq x\leq x_{\max},
$$

entonces una estimación para

$$
x^\ast\in[x_{\min},x_{\max}]
$$

es una interpolación.

Por ejemplo, si tenemos datos para temperaturas entre $20^\circ C$ y $40^\circ C$, estimar el comportamiento a $30^\circ C$ es interpolar.

<br>

### 13.2 Extrapolación

La extrapolación consiste en utilizar el modelo para estimar valores **fuera del rango de los datos observados**.

Si los datos cubren

$$
x_{\min}\leq x\leq x_{\max},
$$

entonces estimar el comportamiento para

$$
x^\ast>x_{\max}
$$

o

$$
x^\ast<x_{\min}
$$

es extrapolar.

Por ejemplo, si tenemos observaciones entre $20^\circ C$ y $40^\circ C$, utilizar el modelo para predecir qué ocurrirá a $80^\circ C$ es una extrapolación.

La extrapolación puede ser mucho más incierta porque estamos suponiendo que el comportamiento observado continúa fuera del intervalo donde tenemos información.

<br>

### 13.3 Comparación

Podemos resumir las tres ideas:

| Concepto | Objetivo | ¿Pasa por los datos? | Región utilizada |
|---|---|---|---|
| Regresión | Encontrar un modelo que represente la tendencia | Generalmente no | Depende del modelo |
| Interpolación | Estimar valores entre datos conocidos | Sí | Dentro del rango observado |
| Extrapolación | Predecir fuera de los datos conocidos | Depende del modelo | Fuera del rango observado |

Es importante notar que **interpolación y extrapolación describen dónde se realiza la estimación**, mientras que regresión describe principalmente **cómo se construye el modelo a partir de los datos**.

Una regresión puede utilizarse posteriormente para interpolar o extrapolar.

<br><br>

## 14. Una perspectiva general para el modelamiento a partir de datos

A partir de los ejemplos anteriores podemos identificar un proceso general.

Partimos de un conjunto de observaciones:

$$
\{(x_i,y_i)\}.
$$

Luego:

1. exploramos visualmente los datos;
2. identificamos posibles relaciones entre las variables;
3. proponemos una familia de modelos;
4. estimamos sus parámetros;
5. evaluamos la calidad del ajuste;
6. analizamos los residuos;
7. validamos el modelo;
8. utilizamos el modelo para interpolar o realizar predicciones;
9. evaluamos cuidadosamente cualquier extrapolación.

La elección del modelo no debe hacerse únicamente buscando el mejor ajuste numérico.

Un modelo matemático debe ser también interpretable y compatible con el fenómeno que estamos estudiando.

<br>

## 15. Ideas principales

- Los datos pueden utilizarse para construir modelos matemáticos.
- La regresión lineal por mínimos cuadrados busca la recta que minimiza la suma de los cuadrados de los residuos.
- Los parámetros de la recta son la pendiente $m$ y el intercepto $b$.
- Los residuos permiten estudiar las diferencias entre los datos observados y las predicciones del modelo.
- El coeficiente $R^2$ proporciona una medida del ajuste, pero no es suficiente por sí solo para validar un modelo.
- La regresión lineal es una herramienta fundamental para construir modelos más generales.
- Los modelos polinomiales son lineales respecto a sus parámetros, aunque no sean lineales respecto a $x$.
- Los modelos exponenciales y de potencia pueden transformarse en modelos lineales mediante logaritmos.
- Cuando una única función no representa adecuadamente diferentes regiones de los datos, podemos construir modelos por tramos.
- Una relación no inyectiva puede seguir siendo una función $y=f(x)$; la falta de inyectividad no impide realizar un ajuste.
- La interpolación busca estimar valores dentro del rango de los datos conocidos.
- La interpolación puede realizarse mediante funciones lineales o polinomios.
- El polinomio de Lagrange permite construir explícitamente un polinomio que pasa por todos los puntos dados.
- La extrapolación consiste en utilizar un modelo fuera del intervalo donde se tienen datos.
- Las extrapolaciones deben interpretarse con especial cuidado, pues dependen de asumir que el comportamiento del modelo continúa fuera del rango observado.

<br><br>

## 16. Ejercicios

### Ejercicio 1. Regresión lineal

Considere los datos

$$
x=(1,2,3,4,5)
$$

y

$$
y=(3,5,7,8,11).
$$

1. Calcule la recta de regresión por mínimos cuadrados.
2. Determine los residuos.
3. Calcule $R^2$.
4. Grafique los datos y la recta de regresión.
5. Utilice el modelo para estimar $y$ cuando $x=4.5$.

<br>

### Ejercicio 2. Interpretación de parámetros

Suponga que un modelo obtenido mediante regresión lineal es

$$
T(t)=2.5t+18,
$$

donde $t$ está medido en horas y $T$ en grados Celsius.

1. ¿Cuál es la interpretación de la pendiente?
2. ¿Cuál es la interpretación del intercepto?
3. ¿Qué temperatura predice el modelo después de $6$ horas?
4. ¿Qué significa físicamente extrapolar este modelo a $t=100$ horas?

<br>

### Ejercicio 3. Modelo exponencial

Los siguientes datos describen el crecimiento de una población:

$$
\begin{array}{c|cccccc}
t & 0 & 1 & 2 & 3 & 4 & 5\\
\hline
P & 100 & 135 & 185 & 250 & 340 & 460
\end{array}
$$

Suponga el modelo

$$
P(t)=Ae^{Bt}.
$$

1. Transforme el modelo utilizando logaritmos.
2. Realice una regresión lineal entre $t$ y $\ln P$.
3. Determine $A$ y $B$.
4. Construya el modelo exponencial.
5. Compare el modelo con los datos.

<br>

### Ejercicio 4. Interpolación lineal

Se conocen los siguientes datos:

$$
(2,5),\qquad(6,13).
$$

1. Construya la función de interpolación lineal.
2. Estime el valor correspondiente a $x=3$.
3. Estime el valor correspondiente a $x=5$.
4. Explique por qué estas estimaciones son interpolaciones.

<br>

### Ejercicio 5. Interpolación de Lagrange

Considere los puntos

$$
(0,2),\qquad(1,4),\qquad(3,1).
$$

1. Construya los polinomios de Lagrange $L_1,L_2,L_3$.
2. Construya el polinomio interpolante.
3. Verifique que el polinomio pasa por los tres puntos.
4. Utilice el polinomio para estimar el valor de $f(2)$.

<br>

### Ejercicio 6. Interpolación y extrapolación

Considere los datos

$$
(1,4),\qquad(2,7),\qquad(3,10),\qquad(4,13).
$$

1. Construya una regresión lineal.
2. Estime $f(2.5)$.
3. Estime $f(6)$.
4. Determine cuál de las dos estimaciones corresponde a una interpolación y cuál a una extrapolación.
5. Explique por qué la segunda estimación requiere asumir que el comportamiento del modelo continúa fuera del intervalo observado.

<br>

### Ejercicio 7. Modelo por tramos

Considere los datos

$$
\begin{array}{c|ccccccccccc}
x&0&1&2&3&4&5&6&7&8&9&10\\
\hline
y&2&5&8&11&14&15&14&11&8&5&2
\end{array}
$$

1. Explique por qué una única recta no representa adecuadamente los datos.
2. Divida los datos en dos regiones.
3. Realice una regresión lineal para cada región.
4. Construya una función por tramos.
5. Grafique los datos y el modelo.
6. Discuta si los dos modelos se unen de manera continua en el punto de transición.

<br><br>

## 17. Hacia los modelos de evolución

En este capítulo hemos estudiado cómo construir modelos matemáticos a partir de datos.

La regresión permite identificar relaciones entre variables y estimar parámetros. La interpolación permite estimar valores dentro del rango de observaciones, mientras que los modelos por tramos permiten representar fenómenos cuyo comportamiento cambia en diferentes regiones.

Sin embargo, muchos fenómenos no se caracterizan solamente por una relación entre variables, sino por la manera en que un sistema **cambia en el tiempo**.

Una población crece, una sustancia se descompone, el precio de un producto cambia, una epidemia se propaga y una inversión evoluciona.

En estos problemas no basta con preguntar

$$
\text{¿qué relación existe entre }x\text{ y }y?
$$

sino que debemos preguntar:

$$
\boxed{
\text{¿cómo cambia el sistema de un instante al siguiente?}
}
$$

Esta pregunta nos llevará al estudio de los **modelos discretos de evolución**, donde las ecuaciones de recurrencia y las iteraciones permiten describir matemáticamente la dinámica de un sistema.
