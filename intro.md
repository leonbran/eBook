---
downloads: []
---

# Generalidades del curso


Las matemáticas permiten construir representaciones de fenómenos y sistemas presentes en la naturaleza, la ciencia, la ingeniería, la economía y la sociedad. El **modelamiento matemático** consiste en establecer conexiones entre estos fenómenos y estructuras matemáticas que permitan describirlos, analizarlos y comprenderlos. Un modelo no es una copia exacta de la realidad, sino una **representación simplificada**, construida a partir de determinados supuestos para capturar los aspectos relevantes de un fenómeno y responder preguntas concretas. Por ello, modelar implica identificar variables, establecer relaciones, formular supuestos, estimar parámetros y analizar las consecuencias del modelo.

> **Modelar es simplificar para comprender.**

En este curso estudiaremos diferentes familias de modelos matemáticos y desarrollaremos herramientas para su **construcción, análisis, interpretación y simulación computacional**. La calidad de un modelo dependerá de su capacidad para representar adecuadamente los aspectos relevantes del fenómeno para el propósito que se persigue, no de la cantidad de detalles que incorpore. La programación será una herramienta transversal que nos permitirá experimentar con los modelos, trabajar con datos, realizar simulaciones, visualizar resultados y explorar fenómenos cuyo comportamiento puede ser difícil de estudiar únicamente mediante métodos analíticos.


## Objetivos del curso

Al finalizar el curso, se espera que el estudiante pueda:

- Formular e interpretar modelos matemáticos a partir de fenómenos y preguntas concretas.
- Desarrollar pensamiento algorítmico para plantear y resolver problemas.
- Analizar las propiedades y el comportamiento de diferentes tipos de modelos.
- Estimar parámetros y utilizar datos para construir y evaluar modelos.
- Utilizar métodos numéricos y herramientas computacionales para analizar modelos.
- Utilizar el lenguaje de programación Python para implementar algoritmos, realizar simulaciones y visualizar resultados.
- Interpretar los resultados de un modelo y reconocer su alcance y limitaciones.


## Estructura del curso

El curso está organizado en seis unidades. Estas unidades presentan una progresión desde las herramientas computacionales básicas y la construcción de modelos a partir de datos, hasta el estudio de sistemas dinámicos y modelos que incorporan incertidumbre.

<br>

### 1. Introducción al modelamiento matemático

El primer capítulo presenta los conceptos fundamentales del modelamiento matemático. Se discute qué es un modelo matemático, cuáles son sus principales componentes y cómo pueden clasificarse los modelos. En particular, se consideran las diferencias entre modelos deterministas y estocásticos, así como entre modelos discretos y continuos.

También se presenta un proceso general para la construcción de modelos matemáticos. Este proceso no se plantea como una secuencia rígida de pasos, sino como un proceso iterativo, en el que los supuestos, parámetros y relaciones matemáticas pueden modificarse a medida que se obtiene nueva información sobre el fenómeno estudiado.

Finalmente, se introduce el papel de la programación científica como herramienta para la exploración, análisis y simulación de modelos.

La pregunta que guiará esta unidad será:

> **¿Cómo podemos construir un modelo matemático que represente de manera adecuada un fenómeno y nos permita comprender y analizar su comportamiento?**



### Unidad 2. Herramientas computacionales

Comenzaremos desarrollando las herramientas computacionales necesarias para trabajar con modelos matemáticos. Aprenderemos a diseñar algoritmos, implementar procedimientos en Python, trabajar con datos y utilizar representaciones gráficas para explorar resultados.

La programación se presentará desde una perspectiva orientada al modelamiento, de manera que cada herramienta computacional pueda utilizarse posteriormente en la construcción, análisis y simulación de modelos.

La pregunta fundamental de esta unidad será:

> **¿Cómo podemos utilizar la programación para explorar y analizar modelos matemáticos?**



### Unidad 3. Modelos por ajuste de datos

En esta unidad estudiaremos modelos construidos a partir de datos. Introduciremos diferentes técnicas de ajuste y regresión para estimar los parámetros de un modelo a partir de observaciones.

Además de construir modelos, aprenderemos a evaluar su capacidad para describir los datos y a distinguir entre ajuste, interpolación, predicción y extrapolación.

La pregunta central será:

> **¿Cómo podemos construir un modelo matemático a partir de datos?**



### Unidad 4. Modelos de cambio discreto

Muchos fenómenos involucran sistemas cuyo estado cambia con el tiempo. Cuando consideramos el tiempo como una variable discreta, podemos describir esta evolución mediante **ecuaciones en diferencias**.

Estudiaremos modelos de crecimiento, modelos poblacionales y sistemas dinámicos discretos. Analizaremos conceptos como puntos de equilibrio, estabilidad y comportamiento caótico, utilizando herramientas gráficas y computacionales para explorar la evolución de los sistemas.

La pregunta que guiará esta unidad será:

> **¿Cómo evoluciona un sistema cuando observamos su estado paso a paso?**



### Unidad 5. Modelos de cambio continuo

En esta unidad pasaremos de una descripción discreta del tiempo a una descripción continua. Las **ecuaciones diferenciales ordinarias** proporcionan un lenguaje natural para modelar sistemas en los que las tasas de cambio determinan su evolución.

Estudiaremos sistemas de ecuaciones diferenciales y modelos provenientes de diferentes áreas de aplicación. Combinaremos el análisis cualitativo con métodos numéricos para aproximar soluciones y explorar el comportamiento de los sistemas.

La pregunta central será:

> **¿Cómo podemos describir matemáticamente la evolución continua de un sistema?**



### Unidad 6. Modelos estocásticos de Poisson

Hasta este punto, los modelos estudiados describen fenómenos cuyo comportamiento puede determinarse a partir de las condiciones del sistema y de sus parámetros. Sin embargo, muchos fenómenos presentan variabilidad e incertidumbre inherentes.

En esta unidad introduciremos los modelos estocásticos  a partir de variables aleatorias y distribuciones de probabilidad. Estudiaremos la distribución de Poisson como una herramienta para modelar el número de eventos que ocurren durante un intervalo de tiempo o espacio, y analizaremos su relación con la distribución binomial.

La pregunta fundamental será:

> **¿Cómo podemos modelar matemáticamente la ocurrencia aleatoria de eventos?**



### Unidad 7. Modelos estocásticos de Markov

La incertidumbre no solo aparece en el número de eventos que ocurren, sino también en la evolución temporal de un sistema. En muchos fenómenos, el estado futuro depende del estado actual y existe una cierta probabilidad de pasar de un estado a otro.

En esta unidad estudiaremos las **cadenas de Markov** como modelos para describir sistemas que evolucionan entre diferentes estados. Analizaremos matrices de transición, trayectorias, distribuciones de estado y simulación. Posteriormente introduciremos las **cadenas de Markov ocultas** y el algoritmo de Viterbi, que permiten inferir estados que no pueden observarse directamente.

La pregunta central será:

> **¿Cómo podemos modelar la evolución de un sistema cuando el cambio entre sus estados es incierto?**




## Sobre estas notas de clase

Estas notas  acompaña el desarrollo del curso y combina conceptos matemáticos, ejemplos, experimentos computacionales y ejercicios. Los ejemplos computacionales pueden ejecutarse y modificarse para explorar directamente el comportamiento de los modelos. La intención no es solamente presentar modelos terminados, sino mostrar **cómo se construyen, cómo se analizan y qué podemos aprender de ellos**.


