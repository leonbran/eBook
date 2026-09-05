# Herramientas computacionales para el modelamiento matemático

En el modelamiento matemático, las herramientas computacionales cumplen un papel fundamental. Una vez construido un modelo, frecuentemente necesitamos realizar cálculos, visualizar funciones y datos, resolver ecuaciones, estimar parámetros o realizar simulaciones.

En este curso utilizaremos principalmente **Python** y **Google Colab** para realizar estas tareas.

El objetivo de este capítulo no es estudiar Python como un lenguaje de programación de manera independiente. En cambio, aprenderemos las herramientas computacionales necesarias para **construir, analizar, simular y visualizar modelos matemáticos**.

La idea central será:

> **El computador será nuestro laboratorio para experimentar con modelos matemáticos.**

A lo largo del capítulo utilizaremos ejemplos sencillos para aprender las herramientas que posteriormente emplearemos en las diferentes unidades del curso.

<br><br>


## 1. El computador como laboratorio matemático

Cuando trabajamos con un modelo matemático, podemos realizar diferentes tipos de experimentos.

Por ejemplo, podemos necesitar calcular valores de una función, construir una tabla de valores, representar gráficamente una expresión matemática, analizar datos o explorar cómo cambia un resultado cuando modificamos determinados parámetros.

Matemáticamente podemos realizar muchas de estas tareas de manera analítica. Sin embargo, un computador permite realizar rápidamente cálculos que pueden resultar tediosos o imposibles de hacer manualmente.

Podemos utilizarlo para:

* realizar cálculos numéricos;
* construir tablas de valores;
* representar funciones gráficamente;
* visualizar datos;
* resolver ecuaciones;
* estimar parámetros;
* realizar simulaciones;
* comparar diferentes escenarios;
* explorar el efecto de modificar parámetros.

Esto transforma el computador en una especie de **laboratorio matemático**.

Podemos formular una pregunta, diseñar un experimento computacional, observar los resultados y modificar nuestras hipótesis o nuestro modelo.

En este curso utilizaremos esta perspectiva de manera sistemática.

<br>







En este curso utilizaremos esta perspectiva de manera sistemática.

<br><br>



##2. Algoritmos: del procedimiento matemático al computador

Cuando resolvemos un problema matemático, generalmente seguimos una serie de pasos para obtener un resultado. Por ejemplo, para calcular el promedio de un conjunto de números debemos sumar sus elementos y dividir el resultado entre la cantidad de elementos.

Cuando queremos que un computador realice este procedimiento, necesitamos describir de manera precisa qué debe hacer y en qué orden debe hacerlo.

Una forma de expresar esta idea es mediante un algoritmo.

Un algoritmo es una secuencia finita y ordenada de instrucciones que permite resolver un problema o realizar una tarea a partir de unos datos de entrada.

Podemos pensar en un algoritmo como una receta matemática: especifica los datos que necesitamos, las operaciones que debemos realizar y la manera de obtener el resultado.

Por ejemplo, supongamos que queremos calcular el promedio de $n$ números

$$ x_1,x_2,\ldots,x_n. $$

Matemáticamente, sabemos que el promedio está dado por

$$ \bar{x}=\frac{1}{n}\sum_{i=1}^{n}x_i. $$

Pero para que un computador pueda realizar este cálculo, necesitamos convertir la expresión matemática en una secuencia de pasos.

Podemos describir el procedimiento de la siguiente manera:

Recibir los números $x_1,x_2,\ldots,x_n$.
Inicializar una variable para almacenar la suma.
Recorrer los números uno por uno.
Agregar cada número a la suma.
Dividir la suma entre $n$.
Mostrar el resultado.

Esta secuencia constituye un algoritmo para calcular el promedio.

<br>

###2.1 Características de un algoritmo

Un algoritmo debe describir un procedimiento de manera suficientemente precisa para que pueda ser ejecutado sin ambigüedades.

Entre sus características fundamentales podemos destacar:

Entrada: los datos que necesita el procedimiento.
Proceso: las operaciones que deben realizarse.
Salida: el resultado que se desea obtener.
Orden: las instrucciones deben ejecutarse siguiendo una secuencia determinada.
Finitud: el procedimiento debe terminar después de un número finito de pasos.
Precisión: cada instrucción debe estar definida de manera clara.

Por ejemplo, para calcular el promedio de una colección de datos:

Entrada:
    x₁, x₂, ..., xₙ

Proceso:
    calcular la suma
    dividir entre n

Salida:
    promedio

Esta estructura de entrada, proceso y salida será recurrente cuando construyamos algoritmos para problemas de modelamiento matemático.

<br>

### 2.2 Algoritmos y matemáticas

Un algoritmo no es necesariamente un programa.

El algoritmo describe el procedimiento que queremos realizar, mientras que un programa es una implementación de ese procedimiento utilizando un lenguaje de programación.

Podemos visualizar la relación de la siguiente manera:

Problema
   ↓
Procedimiento matemático
   ↓
Algoritmo
   ↓
Programa
   ↓
Computador
   ↓
Resultado

Por ejemplo, consideremos la expresión

$$ f(x)=x^2+2x+1. $$

Si queremos evaluar la función en un valor dado de $x$, podemos describir el procedimiento como:

Recibir el valor de $x$.
Calcular $x^2$.
Calcular $2x$.
Sumar $x^2$, $2x$ y $1$.
Mostrar el resultado.

Posteriormente podremos implementar este algoritmo en Python:

x = 3

y = x**2 + 2*x + 1

print(y)

El código es entonces una forma concreta de expresar el algoritmo para que pueda ser ejecutado por el computador.

<br>

### 2.3 Pseudocódigo

Una manera de diseñar un algoritmo antes de escribir el programa es utilizar pseudocódigo.

El pseudocódigo utiliza un lenguaje sencillo, cercano al lenguaje natural, para describir las instrucciones de un algoritmo sin preocuparse todavía por las reglas particulares de Python u otro lenguaje de programación.

Por ejemplo, el algoritmo para calcular el promedio puede escribirse como:

INICIO

    Leer n
    suma ← 0

    Para i desde 1 hasta n:
        Leer x
        suma ← suma + x

    promedio ← suma / n

    Mostrar promedio

FIN

El pseudocódigo permite concentrarnos en la lógica del procedimiento.

Una vez que el algoritmo está correctamente definido, podemos traducirlo a Python:

n = int(input("Cantidad de números: "))

suma = 0

for i in range(n):
    x = float(input("Ingrese un número: "))
    suma = suma + x

promedio = suma / n

print("Promedio:", promedio)

Observemos que la estructura lógica del algoritmo permanece esencialmente igual. Lo que cambia es la forma de expresar las instrucciones.

<br>

### 2.4 Diagramas de flujo

Otra manera de representar un algoritmo es mediante un diagrama de flujo.

Un diagrama de flujo representa gráficamente las diferentes etapas de un procedimiento y las relaciones entre ellas.

Los elementos más comunes son:

┌─────────────┐
│    Inicio   │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│    Entrada  │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│   Proceso   │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│    Salida   │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│     Fin     │
└─────────────┘

En un diagrama de flujo, las flechas indican el orden en que se ejecutan las diferentes instrucciones.

Cuando el algoritmo incluye decisiones, podemos representar una condición:

          ┌─────────────┐
          │ ¿condición? │
          └──────┬──────┘
             Sí  │  No
             ▼   │   ▼
        ┌────────┐ ┌────────┐
        │ Acción │ │ Acción │
        │   A    │ │   B    │
        └────┬───┘ └───┬────┘
             │         │
             └────┬────┘
                  ▼
              Continuar

Los diagramas de flujo son particularmente útiles cuando un procedimiento contiene decisiones, repeticiones o diferentes caminos posibles.

<br>

### 2.5 Algoritmos con decisiones

Muchos problemas matemáticos requieren tomar decisiones dependiendo de los datos.

Por ejemplo, podemos querer determinar si un número es positivo, negativo o cero.

El procedimiento puede describirse como:

INICIO

    Leer x

    Si x > 0:
        Mostrar "positivo"

    Si x < 0:
        Mostrar "negativo"

    Si x = 0:
        Mostrar "cero"

FIN

En Python podemos implementarlo mediante:

x = float(input("Ingrese un número: "))

if x > 0:
    print("positivo")
elif x < 0:
    print("negativo")
else:
    print("cero")

La estructura if, elif y else permite implementar en Python las decisiones que aparecen en el algoritmo.

<br>

### 2.6 Algoritmos con repeticiones

Otros problemas requieren repetir una operación varias veces.

Por ejemplo, supongamos que queremos calcular la suma

$$ S=\sum_{i=1}^{n}i. $$

Podemos describir el algoritmo mediante:

INICIO

    Leer n
    suma ← 0

    Para i desde 1 hasta n:
        suma ← suma + i

    Mostrar suma

FIN

Y podemos implementarlo en Python:

n = 10
suma = 0

for i in range(1, n + 1):
    suma = suma + i

print(suma)

La estructura repetitiva del algoritmo se traduce en Python mediante un ciclo for.

Las repeticiones son especialmente importantes en el modelamiento matemático, pues muchas simulaciones requieren aplicar repetidamente una misma regla.

<br>
2.7 Diseñar antes de programar

Una práctica recomendable es diseñar el algoritmo antes de escribir el código.

Esto permite separar dos preguntas diferentes:

¿Qué procedimiento debemos realizar para resolver el problema?
¿Cómo escribimos ese procedimiento en Python?

La primera pregunta corresponde al diseño del algoritmo. La segunda corresponde a su implementación.

Por ejemplo:

Problema matemático
        ↓
¿Qué queremos calcular?
        ↓
Diseño del algoritmo
        ↓
Pseudocódigo / diagrama de flujo
        ↓
Implementación en Python
        ↓
Ejecución
        ↓
Análisis del resultado

Esta separación ayuda a detectar errores de razonamiento antes de enfrentarnos a errores de programación.

Además, un mismo algoritmo puede implementarse posteriormente en diferentes lenguajes de programación.

<br>

### 2.8 Algoritmos en el modelamiento matemático

En el modelamiento matemático, los algoritmos adquieren una importancia especial porque muchos modelos no pueden resolverse simplemente mediante una fórmula.

Por ejemplo, podemos tener una regla de evolución

$$ x_{n+1}=f(x_n), $$

y querer calcular una sucesión

$$ x_0,x_1,x_2,\ldots,x_N. $$

El modelo matemático proporciona la regla de evolución, pero necesitamos un algoritmo que indique cómo utilizarla:

INICIO

    Definir x₀
    Definir N

    Para n desde 0 hasta N-1:

        calcular xₙ₊₁ = f(xₙ)

        guardar xₙ₊₁

    Mostrar resultados

FIN

Posteriormente este algoritmo puede implementarse en Python y utilizarse para realizar experimentos computacionales.

Esta relación entre modelo matemático, algoritmo y programa será fundamental en las siguientes unidades del curso.




<br><br>


## 3. ¿Qué es Google Colab?

**Google Colab** es un entorno de computación en la nube que permite ejecutar código Python utilizando notebooks interactivos.

Una característica importante de Colab es que el código no necesita ejecutarse directamente en nuestro computador personal. Cuando abrimos un notebook de Colab, podemos conectarnos a un entorno de ejecución remoto proporcionado por Google.

Esta característica resulta especialmente útil en un curso de modelamiento matemático porque permite que los estudiantes trabajen con un entorno computacional común, sin necesidad de instalar Python y las diferentes bibliotecas científicas en sus computadores.

Podemos representar esquemáticamente el funcionamiento de Colab de la siguiente manera:

```text
                    Google Colab
                         │
                         ▼
                  ┌─────────────┐
                  │   Notebook  │
                  └──────┬──────┘
                         │
                  código + datos
                         │
                         ▼
                  ┌─────────────┐
                  │   Runtime   │
                  │             │
                  │ Máquina     │
                  │ virtual     │
                  └──────┬──────┘
                         │
              ┌──────────┼──────────┐
              ▼          ▼          ▼
           Python      NumPy     SciPy
              │          │          │
              └──────────┼──────────┘
                         ▼
                  Modelo matemático
                         │
                         ▼
                  cálculo / simulación
                         │
                         ▼
                    visualización
```

Es importante distinguir varios conceptos que utilizaremos durante el curso.

<br>

### 3.1 Python

**Python** es un lenguaje de programación. Es el lenguaje que utilizaremos para expresar algoritmos y realizar cálculos.

Por ejemplo:

```python
x = 2
y = 3

z = x + y

print(z)
```

El resultado será:

```text
5
```

Python será el lenguaje que utilizaremos para implementar los procedimientos matemáticos y computacionales del curso.

<br>

### 3.2 Jupyter Notebook

Un **notebook** es un documento interactivo que permite combinar texto, fórmulas matemáticas, código, resultados y gráficos.

Una de las ventajas de los notebooks es que podemos explicar un procedimiento matemático y, inmediatamente después, ejecutar el código correspondiente.

Por ejemplo, una celda de texto puede contener:

```markdown
Consideremos la función

$$
f(x)=x^2.
$$
```

y una celda de código puede contener:

```python
x = 3
y = x**2

print(y)
```

El resultado será:

```text
9
```

Esta combinación de texto y código será una característica fundamental de nuestro trabajo.

No queremos simplemente producir programas que calculen resultados. Queremos construir notebooks que **documenten nuestro proceso de trabajo matemático y computacional**.

<br>

### 3.3 Google Colab

**Google Colab** es un servicio que permite trabajar con notebooks utilizando infraestructura computacional remota.

Por tanto:

* Python es el lenguaje de programación;
* Jupyter Notebook proporciona el formato y entorno interactivo;
* Colab proporciona un servicio alojado para ejecutar notebooks;
* el **runtime** es el entorno computacional donde realmente se ejecuta nuestro código.

Esta distinción será importante cuando trabajemos con archivos, bibliotecas y sesiones de ejecución.

<br>

## 4. El entorno de ejecución: el runtime

Cuando ejecutamos una celda en Colab, el código no se ejecuta simplemente "dentro de la página web".

El navegador funciona principalmente como una interfaz. El código es enviado a un **entorno de ejecución**, conocido como *runtime*, donde se encuentra instalado Python y donde se realizan los cálculos.

Podemos pensar en el runtime como una máquina virtual temporal que funciona como nuestro computador durante la sesión.

Por ejemplo, cuando ejecutamos:

```python
a = 10
b = 20

c = a + b

print(c)
```

la variable `a`, la variable `b` y el resultado `c` existen dentro del entorno de ejecución.

<br>

### 4.1 ¿Por qué es importante entender el runtime?

Porque el runtime no debe confundirse con el notebook.

El notebook contiene nuestro código y nuestra explicación. El runtime es el entorno donde ese código se ejecuta.

Podemos imaginarlo así:

```text
Notebook
   │
   │ contiene
   ▼
Código Python
   │
   │ se ejecuta en
   ▼
Runtime
   │
   ├── variables
   ├── archivos
   ├── bibliotecas
   └── resultados
```

Esto explica algunos comportamientos que encontraremos posteriormente.

Por ejemplo, si cerramos o reiniciamos el runtime, las variables que habíamos creado pueden desaparecer.

<br>

### 4.2 Sesiones de ejecución

Durante una sesión podemos definir variables y funciones y utilizarlas posteriormente.

Por ejemplo, primero podemos ejecutar:

```python
a = 5
b = 7
```

y posteriormente:

```python
c = a*b

print(c)
```

obteniendo:

```text
35
```

El segundo bloque funciona porque `a` y `b` existen en el runtime.

Sin embargo, si reiniciamos el runtime, esas variables dejan de existir y tendremos que ejecutar nuevamente las celdas necesarias.

Esta es una razón importante para organizar correctamente nuestros notebooks.

<br>

### 4.3 El orden de ejecución importa

Consideremos:

```python
print(x)
```

Si todavía no hemos definido `x`, Python producirá un error.

En cambio:

```python
x = 10

print(x)
```

funcionará correctamente.

Por esta razón, aunque los notebooks permiten ejecutar las celdas en diferentes órdenes, durante el curso procuraremos mantener una estructura lógica y ejecutar las celdas en el orden en que aparecen.

Una buena práctica consiste en poder reiniciar el runtime y ejecutar nuevamente todas las celdas desde el comienzo sin producir errores.

<br><br>


## 5. Celdas de código y celdas de texto

Los notebooks permiten utilizar diferentes tipos de celdas.

Las dos que utilizaremos principalmente son:

* **celdas de código**, donde escribimos y ejecutamos Python;
* **celdas de texto**, donde escribimos explicaciones, fórmulas y comentarios.

Por ejemplo, una celda de texto puede contener:

```markdown
Consideremos la función

$$
f(x)=x^2+1.
$$
```

y una celda de código puede contener:

```python
x = 3
f = x**2 + 1

print(f)
```

El resultado será:

```text
10
```

La combinación de texto y código permite construir documentos que son simultáneamente **explicativos y ejecutables**.

Esta característica será especialmente importante en nuestro curso, pues queremos que los notebooks sirvan no solamente para ejecutar cálculos, sino también para explicar los procedimientos utilizados y discutir los resultados obtenidos.

<br><br>

## 6. Archivos y almacenamiento

Los modelos matemáticos frecuentemente requieren datos externos.

Por ejemplo, podemos tener un archivo que contiene:

* mediciones experimentales;
* registros;
* temperaturas;
* precios;
* posiciones;
* resultados de experimentos;
* parámetros de un modelo.

Para trabajar con estos datos necesitamos comprender dónde están almacenados nuestros archivos.

<br>

### 6.1 El sistema de archivos del runtime

El runtime de Colab dispone de un sistema de archivos que podemos utilizar durante nuestra sesión.

Podemos observar el contenido de una carpeta utilizando Python:

```python
import os

os.listdir()
```

También podemos crear un archivo:

```python
with open("ejemplo.txt", "w") as archivo:
    archivo.write("Primer experimento")
```

y posteriormente verificar que existe:

```python
os.listdir()
```

Sin embargo, debemos recordar que el sistema de archivos asociado al runtime es temporal.

Por ello, **no debemos asumir que un archivo almacenado allí estará disponible indefinidamente**.

<br>

### 6.2 Google Drive

Colab permite conectar nuestro entorno de ejecución con Google Drive.

Esto resulta útil cuando necesitamos trabajar de manera persistente con archivos.

Conceptualmente podemos pensar en dos espacios diferentes:

```text
Google Drive
     │
     │ archivos persistentes
     ▼
   Colab
     │
     │ acceso durante la sesión
     ▼
  Runtime
```

La distinción entre almacenamiento persistente y almacenamiento temporal será importante cuando trabajemos con conjuntos de datos o notebooks que contengan resultados.

<br>

### 6.3 Subir archivos

También podemos cargar directamente archivos desde nuestro computador.

Por ejemplo:

```python
from google.colab import files

uploaded = files.upload()
```

Esta herramienta permite seleccionar un archivo desde nuestro computador y ponerlo a disposición del runtime.

<br><br>

## 7. Primeros pasos con Python

Ahora que conocemos el entorno de trabajo, comenzaremos a utilizar Python.

No estudiaremos Python como un curso independiente de programación. Introduciremos sus elementos fundamentales a medida que sean necesarios para resolver problemas matemáticos.

<br>

### 7.1 Variables

Una variable permite asociar un nombre con un valor.

Por ejemplo:

```python
P0 = 100
r = 0.05
t = 10
```

En este caso:

* `P0` representa una población inicial;
* `r` representa una tasa de crecimiento;
* `t` representa un instante de tiempo.

Podemos calcular una expresión:

```python
P = P0 * (1 + r*t)

print(P)
```

La elección de nombres significativos será una buena práctica durante todo el curso.

<br>

###7.2 Operaciones matemáticas

Python permite realizar las operaciones aritméticas usuales:

```python
a = 10
b = 3

suma = a + b
resta = a - b
producto = a * b
division = a / b
potencia = a**b
```

La potencia se escribe utilizando `**`.

Por ejemplo:

```python
2**3
```

produce:

```text
8
```

<br>

### 7.3 Funciones matemáticas

Las funciones matemáticas pueden utilizarse mediante bibliotecas especializadas.

Por ejemplo:

```python
import math

x = 2

y = math.exp(x)

print(y)
```

Aquí `math.exp(x)` representa $e^x$.

También podemos utilizar:

```python
math.sqrt(x)
math.sin(x)
math.cos(x)
math.log(x)
```

Estas herramientas serán útiles, aunque para cálculo numérico utilizaremos principalmente **NumPy**.

<br>

### 7.4 Definición de funciones

Una de las estructuras más importantes de Python para el modelamiento matemático es la definición de funciones.

Supongamos que queremos trabajar con

$$
f(x)=x^2+2x+1.
$$

Podemos definir:

```python
def f(x):
    return x**2 + 2*x + 1
```

Ahora podemos evaluar la función:

```python
f(0)
```

o:

```python
f(3)
```

También podemos utilizarla dentro de expresiones:

```python
y = f(5)

print(y)
```

Esta forma de representar funciones matemáticas será utilizada constantemente en el curso.

<br><br>

## 8. Iteraciones y estructuras de control

Los modelos matemáticos y los algoritmos computacionales frecuentemente requieren repetir operaciones.

Python proporciona diferentes estructuras para controlar la ejecución de un programa.


## 2.6 Ciclos: repetir instrucciones

En muchos problemas matemáticos necesitamos realizar una misma operación varias veces. En programación, estas estructuras se conocen como **ciclos** o **bucles**.

En Python existen dos ciclos fundamentales: `for` y `while`.

- `for`: se utiliza cuando conocemos el conjunto de valores o el número de iteraciones.
- `while`: se utiliza cuando la repetición depende de una condición.

<br>

### 2.6.1 El ciclo `for`

El ciclo `for` permite repetir instrucciones para cada elemento de una secuencia.

Por ejemplo, para calcular

$$
S=\sum_{i=1}^{n}i,
$$

podemos escribir el algoritmo:

```text
INICIO

    Leer n
    suma ← 0

    Para i desde 1 hasta n:
        suma ← suma + i

    Mostrar suma

FIN

En Python:

n = 10
suma = 0

for i in range(1, n + 1):
    suma = suma + i

print(suma)

La variable i toma sucesivamente los valores $1,2,\ldots,n$.

Los ciclos for también permiten implementar reglas de evolución. Por ejemplo,

$$ x_{n+1}=\frac{1}{2}x_n+1, \qquad x_0=0. $$
x = 0

for n in range(10):
    x = 0.5 * x + 1
    print(x)

Cada iteración corresponde a un paso en la evolución del sistema.

<br>

2.6.2 El ciclo while

El ciclo while repite instrucciones mientras una condición sea verdadera.

Por ejemplo:

n = 1

while n <= 10:
    print(n)
    n = n + 1

El algoritmo correspondiente es:

INICIO

    n ← 1

    Mientras n ≤ 10:
        Mostrar n
        n ← n + 1

FIN

A diferencia del for, el número de iteraciones no tiene que conocerse previamente.

<br>
2.6.3 for o while?

Podemos establecer como regla práctica:

for: repetir para un conjunto de valores o un número determinado de iteraciones.

while: repetir mientras se cumpla una condición.

Por ejemplo, un for es apropiado cuando queremos realizar exactamente 100 iteraciones:

for n in range(100):
    # instrucciones

Mientras que un while es apropiado cuando queremos continuar hasta alcanzar una determinada condición:

while error > tolerancia:
    # actualizar aproximación
    # calcular nuevo error

Esta segunda situación es especialmente frecuente en los métodos iterativos.

<br>

2.6.4 Ciclos y métodos iterativos

Supongamos que queremos aproximar $\sqrt{2}$ mediante

$$ x_{n+1} = \frac{1}{2} \left( x_n+\frac{2}{x_n} \right). $$

Podemos detener el proceso cuando

$$ |x_n^2-2|<\varepsilon. $$

En Python:

x = 1.0
tolerancia = 1e-8

while abs(x**2 - 2) > tolerancia:
    x = 0.5 * (x + 2/x)

print(x)

Aquí el ciclo continúa hasta que se alcanza la precisión deseada. Este tipo de algoritmo será importante posteriormente en los métodos numéricos y en el modelamiento matemático.

<br>
2.6.5 Cuidado con los ciclos infinitos

Un ciclo while debe modificar las variables involucradas en su condición para que eventualmente pueda terminar.

Por ejemplo, el siguiente ciclo nunca termina:

n = 1

while n <= 10:
    print(n)

La condición siempre es verdadera porque n nunca cambia.

Una versión correcta es:

n = 1

while n <= 10:
    print(n)
    n = n + 1

Por tanto, al diseñar un algoritmo iterativo debemos preguntarnos no solamente qué se repite, sino también qué hace que el ciclo termine.

<br>
2.6.6 Ciclos en el modelamiento matemático

Los ciclos permiten convertir una regla matemática en un procedimiento computacional. Por ejemplo,

$$ x_{n+1}=f(x_n) $$

puede implementarse mediante un ciclo que genere sucesivamente

$$ x_0,x_1,\ldots,x_N. $$

La conexión fundamental es:

Modelo matemático
        ↓
Regla de evolución
        ↓
Algoritmo iterativo
        ↓
Ciclo for / while
        ↓
Programa
        ↓
Simulación

Esta relación entre modelo, algoritmo, ciclo y simulación será recurrente a lo largo del curso.




### 8.1 Condiciones

También podemos hacer que el programa tome decisiones utilizando `if`.

Por ejemplo:

```python
x = 5

if x > 0:
    print("x es positivo")
```

Podemos incluir diferentes posibilidades:

```python
x = -2

if x > 0:
    print("x es positivo")
elif x < 0:
    print("x es negativo")
else:
    print("x es cero")
```

Las estructuras condicionales serán útiles cuando construyamos algoritmos que dependan de determinadas condiciones.

<br>

### 8.2 Listas

Las listas permiten almacenar varios objetos.

Por ejemplo:

```python
valores = [1, 2, 3, 4, 5]
```

Podemos acceder a un elemento:

```python
valores[0]
```

que produce:

```text
1
```

También podemos agregar elementos:

```python
valores.append(6)
```

Las listas son útiles para almacenar resultados obtenidos durante una simulación o un cálculo.

<br>

## 9. NumPy: cálculo numérico

Para realizar cálculo científico utilizaremos principalmente el modulo **NumPy**. NumPy proporciona estructuras y operaciones eficientes para trabajar con arreglos numéricos, vectores y matrices.

La importación habitual es:

```python
import numpy as np
```

El alias `np` es una convención ampliamente utilizada en Python científico.

<br>

### 9.1 Arreglos

Podemos construir un arreglo:

```python
x = np.array([1, 2, 3, 4, 5])
```

Este objeto puede interpretarse matemáticamente como un vector:

$$
x=
\begin{pmatrix}
1\\
2\\
3\\
4\\
5
\end{pmatrix}.
$$

Podemos realizar operaciones:

```python
x + 2
```

o:

```python
2*x
```

También podemos calcular:

```python
np.sum(x)
```

y:

```python
np.mean(x)
```

<br>

### 9.2 Operaciones vectorizadas

Una de las ventajas fundamentales de NumPy es que podemos aplicar una operación a todos los elementos de un arreglo simultáneamente.

Por ejemplo:

```python
x = np.array([0, 1, 2, 3, 4])

y = x**2
```

El resultado es equivalente a calcular

$$
y_i=x_i^2
$$

para cada componente.

También podemos escribir:

```python
y = np.exp(x)
```

para obtener

$$
y_i=e^{x_i}.
$$

Esta capacidad, conocida como **vectorización**, será especialmente importante para trabajar con funciones y datos.

<br>

### 9.3 Crear mallas de puntos

Supongamos que queremos representar la función

$$
f(x)=x^2
$$

en el intervalo $[-2,2]$.

Necesitamos construir un conjunto de valores de $x$.

Podemos utilizar:

```python
x = np.linspace(-2, 2, 100)
```

Esto genera 100 puntos distribuidos uniformemente entre $-2$ y $2$.

Posteriormente podemos calcular:

```python
y = x**2
```

Ahora `x` contiene los valores de entrada y `y` contiene los valores correspondientes de la función.

Esta operación aparecerá continuamente cuando construyamos gráficas.

<br>

### 9.4 Vectores y matrices

NumPy también permite representar matrices.

Por ejemplo:

```python
A = np.array([
    [1, 2],
    [3, 4]
])
```

representa

$$
A=
\begin{pmatrix}
1&2\\
3&4
\end{pmatrix}.
$$

Podemos definir un vector:

```python
x = np.array([5, 6])
```

y calcular el producto matricial:

```python
A @ x
```

Este tipo de operaciones será especialmente útil cuando estudiemos sistemas de ecuaciones y modelos que involucren álgebra lineal.

<br><br>

## 10. Visualización de datos con Matplotlib

Una de las herramientas más importantes para estudiar modelos matemáticos es la visualización.

Una gráfica puede revelar rápidamente:

* tendencias;
* crecimiento;
* oscilaciones;
* estabilidad;
* cambios de comportamiento;
* relaciones entre variables;
* diferencias entre resultados.

Utilizaremos principalmente **Matplotlib**.

La importación habitual es:

```python
import matplotlib.pyplot as plt
```

<br>

### 10.1 Graficar una función

Consideremos nuevamente

$$
f(x)=x^2.
$$

Podemos construir la gráfica mediante:

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(-2, 2, 100)
y = x**2

plt.plot(x, y)

plt.xlabel("x")
plt.ylabel("f(x)")
plt.title("La función f(x) = x²")

plt.show()
```

La estructura general es:

```text
definir los valores de x
        ↓
calcular y = f(x)
        ↓
graficar x contra y
        ↓
etiquetar
        ↓
mostrar
```

<br>

### 10.2 Comparar funciones

También podemos comparar diferentes funciones.

Por ejemplo:

$$
f(x)=x^2,
\qquad
g(x)=2x+1.
$$

En Python:

```python
x = np.linspace(-2, 2, 100)

f = x**2
g = 2*x + 1

plt.plot(x, f, label="f(x) = x²")
plt.plot(x, g, label="g(x) = 2x + 1")

plt.xlabel("x")
plt.ylabel("y")
plt.legend()

plt.show()
```

La posibilidad de comparar diferentes funciones será muy útil cuando estudiemos diferentes modelos matemáticos.

<br>

### 10.3 Datos experimentales

Las gráficas también permiten representar datos.

Supongamos que tenemos las observaciones:

```python
t = np.array([0, 1, 2, 3, 4])
P = np.array([100, 108, 121, 135, 151])
```

Podemos representarlas mediante:

```python
plt.scatter(t, P)

plt.xlabel("Tiempo")
plt.ylabel("Población")

plt.show()
```

Posteriormente podemos superponer diferentes representaciones o modelos y comparar sus resultados.

Esta comparación entre **datos y modelos** será una idea central en la unidad de regresión.

<br><br>

## 11. Pandas: trabajar con datos

Cuando los datos provienen de experimentos o bases de datos, frecuentemente necesitamos organizarlos en tablas.

Para ello utilizaremos **Pandas**.

La importación habitual es:

```python
import pandas as pd
```

<br>

### 11.1 DataFrames

Podemos crear una tabla:

```python
datos = {
    "tiempo": [0, 1, 2, 3, 4],
    "poblacion": [100, 108, 121, 135, 151]
}

df = pd.DataFrame(datos)

print(df)
```

El resultado tiene una estructura similar a:

```text
   tiempo  poblacion
0       0        100
1       1        108
2       2        121
3       3        135
4       4        151
```

Un objeto `DataFrame` puede interpretarse como una tabla de datos.

<br>

### 11.2 Seleccionar columnas

Podemos acceder a una columna:

```python
df["tiempo"]
```

o:

```python
df["poblacion"]
```

También podemos utilizar estas columnas para realizar cálculos.

Por ejemplo:

```python
df["poblacion"].mean()
```

calcula la población promedio de los datos.

<br>

### 11.3 Leer datos desde un archivo

Una situación frecuente será recibir datos en un archivo CSV.

Podemos utilizar:

```python
df = pd.read_csv("datos.csv")
```

Una vez cargados los datos podemos inspeccionarlos mediante:

```python
df.head()
```

Esta operación muestra las primeras filas.

También podemos utilizar:

```python
df.describe()
```

para obtener un resumen estadístico básico.

<br>

## 12. SciPy: herramientas científicas

NumPy proporciona las estructuras fundamentales para el cálculo numérico, mientras que **SciPy** proporciona numerosas herramientas científicas adicionales.

Entre ellas encontramos métodos para:

* optimización;
* integración numérica;
* resolución de ecuaciones;
* estadística;
* interpolación;
* ecuaciones diferenciales.

La biblioteca puede importarse mediante:

```python
import scipy
```

No estudiaremos todas sus funcionalidades. Introduciremos aquellas que sean necesarias para los modelos del curso.

<br>

## 13. Buenas prácticas para notebooks científicos

A medida que los notebooks se vuelvan más complejos, será importante seguir algunas reglas básicas.

<br>

### 13.1 Explicar el código

No debemos escribir únicamente código.

Cada notebook debe indicar con claridad:

* qué problema estamos estudiando;
* qué procedimiento estamos realizando;
* qué significan las variables;
* qué parámetros estamos utilizando;
* qué queremos observar;
* cuáles son las conclusiones obtenidas.

Un notebook científico debe poder ser leído por otra persona y permitirle comprender qué se hizo y por qué.

<br>

### 13.2 Utilizar nombres claros

Es preferible utilizar nombres de variables que indiquen su significado.

Por ejemplo:

```python
poblacion_inicial = 100
```

es generalmente más claro que:

```python
a = 100
```

cuando `a` no tiene un significado evidente.

Los nombres deben ayudar a comprender el procedimiento que estamos implementando.

<br>

### 13.3 Separar parámetros y cálculos

Cuando trabajemos con procedimientos que dependen de determinados valores, es recomendable definir esos valores en una sección claramente identificable.

Por ejemplo:

```python
a = 0
b = 10
N = 100
```

y posteriormente utilizar estas cantidades en los cálculos.

Esto facilita modificar los experimentos sin tener que buscar los valores dentro de todo el código.

<br>

### 13.4 Etiquetar las gráficas

Una gráfica científica debe indicar claramente qué representa cada eje.

Por ejemplo:

```python
plt.xlabel("Tiempo")
plt.ylabel("Variable")
```

Cuando sea necesario, podemos agregar un título:

```python
plt.title("Resultado de la simulación")
```

Cuando se comparan varias curvas, debemos utilizar una leyenda:

```python
plt.legend()
```

Una gráfica debe ser comprensible incluso cuando se observa de manera independiente del código que la produjo.

<br>

### 13.5 Mantener una estructura lógica

Un notebook debería seguir una estructura coherente.

Por ejemplo:

```text
1. Planteamiento del problema
2. Definición de variables
3. Parámetros
4. Procedimiento
5. Cálculos
6. Visualización
7. Análisis
8. Conclusiones
```

No todos los notebooks necesitarán exactamente esta estructura, pero la organización debe permitir seguir fácilmente el razonamiento.

<br>

### 13.6 Reiniciar y ejecutar nuevamente

Una práctica importante consiste en verificar que el notebook pueda ejecutarse desde el comienzo.

Esto permite detectar dependencias ocultas entre celdas.

Una estrategia recomendable es:

1. reiniciar el runtime;
2. ejecutar las celdas en orden;
3. verificar que no aparezcan errores;
4. comprobar que los resultados sean reproducibles.

Esta práctica es particularmente importante cuando compartimos nuestros notebooks con otras personas.

<br>

# 14. Colab como herramienta transversal del curso

A partir de este capítulo, Google Colab será nuestro principal entorno de experimentación computacional.

Cada una de las unidades matemáticas del curso utilizará estas herramientas de manera progresiva.

En **modelos por regresión**, utilizaremos Python, NumPy, Pandas, Matplotlib y SciPy para analizar datos, construir representaciones y estimar parámetros.

En **modelos discretos de evolución**, utilizaremos funciones, estructuras de control y herramientas numéricas para estudiar sistemas que evolucionan paso a paso.

En **modelos continuos**, utilizaremos herramientas numéricas para aproximar y visualizar soluciones de ecuaciones diferenciales.

En **modelos estocásticos**, utilizaremos generación de números aleatorios, simulaciones y herramientas estadísticas para estudiar sistemas que incorporan incertidumbre.

Por tanto, las herramientas computacionales no constituyen una unidad aislada del curso. Este capítulo proporciona las herramientas básicas que utilizaremos transversalmente en todas las unidades posteriores.


<br><br>

## 15. Ejercicios

### Ejercicio 1. Evaluación de una función

Considere la función

$$
f(x)=x^3-2x+1.
$$

1. Defina la función en Python.
2. Calcule $f(0)$, $f(1)$ y $f(2)$.
3. Construya 100 puntos igualmente espaciados en el intervalo $[-2,2]$.
4. Calcule la función en esos puntos.
5. Realice la gráfica de $f$.

<br>

### Ejercicio 2. Funciones y visualización

Considere las funciones

$$
f(x)=x^2,
\qquad
g(x)=x^3.
$$

1. Defina ambas funciones en Python.
2. Construya 200 puntos igualmente espaciados en el intervalo $[-2,2]$.
3. Calcule los valores de ambas funciones.
4. Represente las dos funciones en una misma gráfica.
5. Agregue etiquetas para los ejes y una leyenda.

<br>

### Ejercicio 3. Arreglos y operaciones vectorizadas

Considere el arreglo

```python
x = np.array([1, 2, 3, 4, 5])
```

1. Calcule $2x$.
2. Calcule $x^2$.
3. Calcule $e^x$.
4. Calcule la suma de sus elementos.
5. Calcule el promedio de sus elementos.

Realice las operaciones utilizando NumPy.

<br>

### Ejercicio 4. Datos

Considere los siguientes datos:

```python
tiempo = [0, 1, 2, 3, 4, 5]
temperatura = [20.1, 21.3, 22.7, 23.5, 24.8, 26.1]
```

1. Construya un `DataFrame` utilizando Pandas.
2. Muestre las primeras filas de la tabla.
3. Calcule la temperatura promedio.
4. Realice un diagrama de dispersión.
5. Etiquete adecuadamente los ejes.

<br>

### Ejercicio 5. Primer notebook científico

Construya un notebook que estudie una función matemática de su elección.

El notebook debe contener:

1. una breve explicación del problema;
2. la definición matemática de la función;
3. la definición de la función en Python;
4. la construcción de un conjunto de puntos;
5. la evaluación de la función;
6. una gráfica;
7. una breve interpretación de los resultados.

El objetivo no es solamente obtener una gráfica, sino construir un notebook que combine **matemáticas, código, resultados e interpretación**.

<br>



## 15. Ideas principales de este capitulo

Al finalizar este capítulo debemos tener presentes las siguientes ideas:

* **Python** es el lenguaje de programación que utilizaremos para realizar cálculos y construir algoritmos.
* **Jupyter Notebook** permite combinar texto, matemáticas, código y resultados en un mismo documento.
* **Google Colab** proporciona un entorno en la nube para ejecutar nuestros notebooks.
* El **runtime** es el entorno computacional donde realmente se ejecuta nuestro código.
* El runtime debe distinguirse del notebook y puede ser temporal.
* Los archivos almacenados en el entorno de ejecución no deben considerarse almacenamiento permanente.
* **NumPy** proporciona herramientas fundamentales para el cálculo numérico.
* **Matplotlib** permite visualizar funciones, datos y resultados.
* **Pandas** facilita la organización y manipulación de datos.
* **SciPy** proporciona herramientas para diferentes problemas científicos y numéricos.
* Las estructuras de control de Python permiten construir algoritmos y repetir operaciones.
* La programación permite transformar procedimientos matemáticos en **experimentos computacionales**.
* La visualización es una herramienta fundamental para explorar y comunicar resultados.
* La computación y el análisis matemático son herramientas complementarias.
* Los notebooks deben documentar no solamente **qué código ejecutamos**, sino también **qué problema estamos estudiando, qué procedimiento seguimos y qué conclusiones obtenemos**.

<br>
