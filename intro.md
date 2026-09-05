# Introducción al Modelamiento Matemático

<br>

Las matemáticas permiten construir representaciones de fenómenos y sistemas que encontramos en la naturaleza, la ciencia, la ingeniería, la economía y la sociedad. El **modelamiento matemático** busca establecer conexiones entre estos fenómenos y las estructuras matemáticas que permiten describirlos, analizarlos y comprenderlos.

Un modelo matemático no es una copia exacta de la realidad. Es una **representación simplificada**, construida a partir de ciertos supuestos, que busca capturar los aspectos esenciales de un fenómeno para responder preguntas concretas.

El proceso de modelamiento involucra, por tanto, mucho más que encontrar una ecuación: requiere identificar las variables relevantes, establecer relaciones entre ellas, estimar parámetros, analizar las consecuencias del modelo y contrastar sus resultados con los datos o con el comportamiento observado.

En este curso estudiaremos diferentes familias de modelos matemáticos y desarrollaremos herramientas para su construcción, análisis y simulación computacional. La programación será utilizada como una herramienta para explorar los modelos, realizar experimentos numéricos, visualizar resultados y analizar fenómenos que difícilmente pueden estudiarse de manera puramente analítica.

<br>


## Objetivos del curso

Al finalizar el curso, se espera que el estudiante pueda:

- Identificar los elementos fundamentales de un problema de modelamiento.
- Formular modelos matemáticos a partir de fenómenos y preguntas concretas.
- Interpretar las variables y parámetros de un modelo.
- Analizar las propiedades matemáticas de diferentes tipos de modelos.
- Estimar parámetros a partir de datos.
- Utilizar métodos numéricos y herramientas computacionales para estudiar modelos.
- Implementar simulaciones y visualizar sus resultados mediante Python.
- Evaluar las limitaciones y el alcance de un modelo.
- Interpretar los resultados matemáticos en el contexto del fenómeno estudiado.

<br><br>



## Estructura del curso

El curso está organizado en cinco unidades. Estas unidades presentan una progresión desde la construcción básica de modelos hasta la incorporación de dinámica e incertidumbre.


<br>

### Unidad 1. Elementos de programación

Se introducen las herramientas computacionales necesarias para implementar, explorar y analizar modelos matemáticos. Mediante **Python** y **Google Colab**, se desarrollan habilidades básicas para realizar cálculos numéricos, trabajar con datos, visualizar resultados y construir algoritmos. La programación se concibe como una herramienta transversal que permite experimentar con los modelos, analizar su comportamiento y contrastar los resultados obtenidos.

> **¿Cómo podemos utilizar un computador para construir, explorar y comprender un modelo matemático?**





<br>

### Unidad 2. Introducción al modelamiento matemático

Comenzaremos estudiando qué es un modelo matemático y cómo se construye. Analizaremos el papel de las variables, los parámetros, los supuestos y las escalas, así como los procesos de calibración y validación.

La pregunta fundamental de esta unidad será:

> **¿Cómo podemos transformar una pregunta sobre un fenómeno en un problema matemático?**

<br>

### Unidad 3. Modelos por regresión

En esta unidad estudiaremos modelos construidos a partir de datos. Introduciremos la regresión lineal y diferentes extensiones, utilizando herramientas de optimización y mínimos cuadrados para estimar los parámetros de un modelo.

Además de construir modelos, aprenderemos a evaluar su capacidad para describir los datos y a distinguir entre ajuste, predicción y extrapolación.

La pregunta central será:

> **¿Cómo podemos construir un modelo matemático a partir de datos?**

<br>

### Unidad 4. Modelos discretos

Muchos fenómenos involucran sistemas cuyo estado cambia con el tiempo. Cuando consideramos el tiempo como una variable discreta, podemos describir esta evolución mediante **ecuaciones en diferencias**.

Estudiaremos modelos de crecimiento, modelos poblacionales y sistemas dinámicos discretos. Analizaremos conceptos como puntos de equilibrio, estabilidad, bifurcaciones y comportamiento caótico.

La pregunta que guiará esta unidad será:

> **¿Cómo evoluciona un sistema cuando observamos su estado paso a paso?**

<br>

### Unidad 5. Modelos continuos

En esta unidad pasaremos de una descripción discreta del tiempo a una descripción continua. Las **ecuaciones diferenciales ordinarias** proporcionan un lenguaje natural para modelar sistemas en los que las tasas de cambio determinan su evolución.

Estudiaremos modelos de crecimiento y decaimiento, sistemas de ecuaciones diferenciales y modelos provenientes de diferentes áreas de aplicación. Combinaremos el análisis cualitativo con métodos numéricos para aproximar soluciones y explorar el comportamiento de los sistemas.

La pregunta central será:

> **¿Cómo podemos describir matemáticamente la evolución continua de un sistema?**

<br>

### Unidad 6. Modelos estocásticos

En muchos fenómenos existe incertidumbre inherente o información que no podemos conocer con exactitud. En estos casos, los modelos deterministas pueden resultar insuficientes y es necesario incorporar elementos aleatorios.

Introduciremos modelos estocásticos mediante variables aleatorias, simulación, caminatas aleatorias y cadenas de Markov. Estudiaremos cómo la incertidumbre puede incorporarse a modelos de evolución y cómo interpretar los resultados de múltiples simulaciones.

La pregunta fundamental será:

> **¿Cómo incorporamos la incertidumbre en un modelo matemático?**

<br><br>




## Sobre estas notas de clase

Estas notas  acompaña el desarrollo del curso y combina conceptos matemáticos, ejemplos, experimentos computacionales y ejercicios. Los ejemplos computacionales pueden ejecutarse y modificarse para explorar directamente el comportamiento de los modelos. La intención no es solamente presentar modelos terminados, sino mostrar **cómo se construyen, cómo se analizan y qué podemos aprender de ellos**.

> **Modelar es simplificar para comprender.**
>
> La calidad de un modelo no depende de que reproduzca todos los detalles de la realidad, sino de que sea capaz de capturar aquellos aspectos relevantes para la pregunta que queremos responder.
