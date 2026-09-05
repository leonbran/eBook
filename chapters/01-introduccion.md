# Introducción

El **modelamiento matemático** es una herramienta fundamental para estudiar fenómenos y sistemas provenientes de las ciencias naturales, la ingeniería, las ciencias sociales, la economía y muchas otras áreas del conocimiento. Su propósito es construir representaciones matemáticas que permitan comprender, analizar, simular y, en determinadas circunstancias, predecir el comportamiento de un sistema.

En este capítulo presentaremos una introducción general al modelamiento matemático. Comenzaremos discutiendo qué es un modelo matemático y cuáles son sus principales componentes. Posteriormente, estudiaremos algunas formas de clasificar los modelos, en particular según la presencia o ausencia de incertidumbre y según la naturaleza discreta o continua de las variables.

También discutiremos un proceso general para la construcción de modelos matemáticos. Es importante señalar desde el comienzo que este proceso no debe entenderse como una secuencia rígida de pasos. En la práctica, la construcción de un modelo es un proceso **iterativo**, en el que los supuestos, los parámetros y las ecuaciones pueden modificarse a medida que se obtiene nueva información sobre el fenómeno.

Finalmente, introduciremos el papel de la programación científica en el modelamiento matemático y presentaremos **Python** y **Google Colab** como herramientas que utilizaremos a lo largo del curso.

<br><br>

## ¿Qué es un modelo matemático?

Un modelo matemático es una **representación simplificada de un fenómeno, sistema o proceso** mediante conceptos, estructuras y herramientas matemáticas. Su propósito es capturar aquellos aspectos del sistema que son relevantes para responder una pregunta determinada.

Un modelo no pretende reproducir todos los detalles de la realidad. Por el contrario, se construye seleccionando las características que consideramos importantes y realizando determinados supuestos y aproximaciones.

Por ejemplo, si queremos estudiar el movimiento de un objeto que es lanzado al aire, podemos considerar su posición, velocidad y aceleración, y formular relaciones matemáticas entre estas cantidades. Dependiendo de la pregunta que queramos responder, podemos ignorar algunos efectos, como la resistencia del aire, o incorporarlos posteriormente.

Esta idea es fundamental:

> **Un modelo matemático no es la realidad; es una representación de aquellos aspectos de la realidad que consideramos relevantes para una pregunta determinada.**

Los modelos matemáticos son utilizados en numerosas disciplinas. Algunos ejemplos incluyen:

- el movimiento de cuerpos en física;
- el crecimiento y decrecimiento de poblaciones;
- la propagación de enfermedades;
- la dinámica de ecosistemas;
- los mercados financieros;
- los procesos químicos;
- los fenómenos meteorológicos;
- las redes de comunicación;
- los sistemas de transporte;
- el análisis de datos y la inteligencia artificial.

Los modelos permiten estudiar diferentes escenarios, realizar predicciones, analizar relaciones entre variables y tomar decisiones fundamentadas. En muchos casos, sus resultados pueden compararse con datos experimentales u observaciones para evaluar qué tan adecuadamente representan el fenómeno estudiado.

<br><br>

## Componentes de un modelo matemático

Aunque la estructura de un modelo depende del fenómeno y de la pregunta que se quiera estudiar, podemos identificar algunos elementos que aparecen con frecuencia.

### Variables

Las **variables** representan cantidades que pueden cambiar dentro del sistema. Dependiendo del modelo, pueden representar magnitudes físicas, características de una población, estados de un sistema, cantidades económicas o cualquier otra propiedad que resulte relevante.

Por ejemplo, en un modelo de crecimiento poblacional podemos utilizar una variable $P(t)$ para representar el tamaño de una población en el tiempo $t$.

Las variables pueden clasificarse, entre otras formas, en:

- **Variables independientes:** actúan como entradas o cantidades respecto de las cuales se estudia el comportamiento de otras variables.
- **Variables dependientes:** representan cantidades cuyo comportamiento está determinado por otras variables del modelo.

<br>

### Parámetros

Los **parámetros** son cantidades que caracterizan el comportamiento del modelo y que, dentro de un determinado problema, permanecen constantes.

Por ejemplo, en el modelo

$$
\frac{dP}{dt}=rP,
$$

la cantidad $r$ es un parámetro que representa la tasa de crecimiento de la población.

Los parámetros pueden ser conocidos a partir de principios físicos, químicos o biológicos, o pueden necesitar ser **estimados a partir de datos** mediante técnicas estadísticas, métodos de optimización u otros procedimientos matemáticos.

<br>

### Relaciones matemáticas

Las relaciones matemáticas establecen cómo se relacionan las variables y los parámetros del modelo. Estas relaciones pueden adoptar diferentes formas dependiendo de la naturaleza del problema.

Por ejemplo, un modelo puede estar constituido por:

- ecuaciones algebraicas;
- ecuaciones diferenciales;
- ecuaciones en diferencias;
- sistemas de ecuaciones;
- relaciones probabilísticas;
- reglas de transición;
- redes o grafos.

En términos generales, podemos pensar en un modelo matemático como una estructura que relaciona variables y parámetros mediante determinadas reglas matemáticas.

<br>

<!-- ESPACIO PARA GRÁFICO: Componentes de un modelo matemático -->

<br><br>

## Clasificación de los modelos matemáticos

Existen diferentes formas de clasificar los modelos matemáticos. En este curso utilizaremos principalmente dos criterios:

1. la presencia o ausencia de incertidumbre;
2. la naturaleza discreta o continua de las variables.

Estos dos criterios son independientes. Por ejemplo, un modelo puede ser simultáneamente **determinístico y discreto**, **determinístico y continuo**, **estocástico y discreto** o **estocástico y continuo**.

<br>

### Modelos deterministas

Un modelo **determinista** es aquel en el que, una vez especificados los parámetros y las condiciones iniciales, la evolución del sistema queda completamente determinada.

En consecuencia, si repetimos una simulación utilizando exactamente los mismos parámetros y condiciones iniciales, obtendremos el mismo resultado.

Por ejemplo, consideremos el modelo

$$
\frac{dP}{dt}=rP.
$$

Si conocemos el valor de $r$ y la condición inicial $P(0)$, entonces la solución queda determinada.

Algunas características de los modelos deterministas son:

- **Previsibilidad:** dadas las condiciones iniciales y los parámetros, el modelo produce una evolución determinada.
- **Ausencia de aleatoriedad explícita:** el modelo no incorpora variables aleatorias como parte de su formulación.
- **Formalismo matemático:** pueden utilizar ecuaciones algebraicas, ecuaciones diferenciales, ecuaciones en diferencias, sistemas dinámicos, redes y grafos, entre otras estructuras.

Algunos ejemplos de modelos deterministas son:

- movimiento de un proyectil;
- modelos de crecimiento poblacional;
- modelos de movimiento planetario;
- modelos de propagación de enfermedades;
- modelos de equilibrio químico.

<br>

### Modelos estocásticos

Los modelos **estocásticos** incorporan incertidumbre o aleatoriedad en la descripción del fenómeno. En estos modelos, incluso cuando se utilizan las mismas condiciones iniciales y parámetros, diferentes realizaciones pueden producir resultados diferentes.

Por ejemplo, una caminata aleatoria puede utilizarse para representar el movimiento de una partícula cuando la dirección de cada paso está determinada aleatoriamente.

Algunas características de los modelos estocásticos son:

- **Incorporación de incertidumbre:** incluyen elementos aleatorios que influyen en la evolución del sistema.
- **Variabilidad en los resultados:** diferentes realizaciones del mismo modelo pueden producir resultados distintos.
- **Formalismo probabilístico:** pueden utilizar variables aleatorias, distribuciones de probabilidad, procesos estocásticos y cadenas de Markov, entre otras herramientas.

Algunos ejemplos de modelos estocásticos son:

- modelos de caminata aleatoria;
- simulaciones de Monte Carlo;
- modelos de evolución de poblaciones con incertidumbre;
- modelos financieros;
- cadenas de Markov;
- modelos de propagación de enfermedades que incorporan variabilidad aleatoria.

<br>

### Modelos discretos y continuos

Otra forma importante de clasificar los modelos depende de la naturaleza de sus variables.

Un modelo es **discreto** cuando las variables toman valores en conjuntos discretos o cuando la evolución del sistema se describe en instantes separados.

Por ejemplo, una población puede representarse mediante una sucesión

$$
P_0,P_1,P_2,\ldots
$$

donde $P_n$ representa el tamaño de la población después de $n$ generaciones.

Un modelo continuo, por otro lado, describe variables que pueden cambiar continuamente y tomar valores en un intervalo de los números reales.

Por ejemplo, podemos representar el tamaño de una población mediante una función

$$
P(t), \qquad t\in [0,T],
$$

donde $t$ representa el tiempo.

Los modelos discretos suelen conducir naturalmente a **ecuaciones en diferencias**, mientras que los modelos continuos pueden conducir a **ecuaciones diferenciales**.

Es importante observar que esta clasificación es independiente de la clasificación entre determinista y estocástico. Por ejemplo:

- una ecuación en diferencias determinista produce un modelo determinista y discreto;
- una ecuación diferencial determinista produce un modelo determinista y continuo;
- una caminata aleatoria produce un modelo estocástico y discreto;
- un proceso estocástico continuo puede producir un modelo estocástico y continuo.

<br>

<!-- ESPACIO PARA GRÁFICO: Clasificación de los modelos matemáticos -->

<br><br>

## Un proceso para la construcción de modelos matemáticos

La construcción de un modelo matemático depende del fenómeno estudiado, de la información disponible y de la pregunta que queremos responder. Por esta razón, no existe un procedimiento único que pueda aplicarse a todos los problemas.

Sin embargo, podemos identificar algunas etapas que aparecen con frecuencia en el proceso de modelamiento.

Es importante entender estas etapas como parte de un **proceso iterativo**. En la práctica, podemos regresar a etapas anteriores cuando los resultados obtenidos indican que es necesario modificar los supuestos, incorporar nuevas variables o utilizar una formulación matemática diferente.

<br>

### 1. Definición del problema

El primer paso consiste en identificar con claridad el fenómeno que queremos estudiar y formular la pregunta que deseamos responder.

En esta etapa debemos establecer el contexto del problema, delimitar el alcance del modelo e identificar las cantidades que consideramos relevantes.

También es necesario formular los primeros **supuestos simplificadores**. Estos supuestos permiten transformar una situación real, generalmente compleja, en un problema que pueda ser tratado matemáticamente.

<br>

### 2. Identificación de las variables y los parámetros

Una vez definido el problema, debemos determinar qué cantidades serán representadas mediante variables y cuáles actuarán como parámetros del modelo.

La elección de las variables es una parte fundamental del proceso de modelamiento. Una elección inadecuada puede conducir a un modelo innecesariamente complejo o incapaz de representar los aspectos esenciales del fenómeno.

<br>

### 3. Recopilación y análisis de datos

Cuando los datos están disponibles, estos pueden proporcionar información fundamental para la construcción y evaluación del modelo.

Los datos pueden obtenerse mediante experimentos, observaciones, registros históricos, sensores, bases de datos u otras fuentes.

Los datos pueden utilizarse para:

- identificar relaciones entre variables;
- estimar parámetros;
- calibrar el modelo;
- evaluar sus predicciones;
- comparar diferentes modelos;
- validar los resultados.

Sin embargo, no todos los modelos matemáticos parten de datos. Algunos se construyen principalmente a partir de principios físicos, químicos, biológicos o de otras teorías científicas.

<br>

### 4. Formulación del modelo matemático

En esta etapa se establecen las relaciones matemáticas que describen el fenómeno.

Dependiendo del problema, podemos utilizar ecuaciones algebraicas, ecuaciones diferenciales, ecuaciones en diferencias, sistemas de ecuaciones, modelos probabilísticos u otras estructuras matemáticas.

La formulación debe ser suficientemente sencilla para permitir su análisis y, al mismo tiempo, suficientemente rica para capturar los aspectos relevantes del fenómeno.

<br>

### 5. Análisis del modelo

Una vez formulado el modelo, podemos estudiar sus propiedades matemáticas.

Dependiendo del tipo de modelo, esto puede incluir:

- encontrar soluciones;
- estudiar puntos de equilibrio;
- analizar estabilidad;
- estudiar sensibilidad respecto a los parámetros;
- determinar comportamientos a largo plazo;
- analizar incertidumbre;
- estudiar propiedades cualitativas de las soluciones.

El análisis matemático permite comprender las consecuencias de los supuestos realizados y obtener información sobre el comportamiento del sistema.

<br>

### 6. Calibración y ajuste

Cuando el modelo contiene parámetros desconocidos, estos pueden estimarse utilizando datos.

El proceso de **calibración** o **ajuste** busca determinar valores de los parámetros que permitan que el modelo reproduzca adecuadamente las observaciones disponibles.

Para ello pueden utilizarse métodos como:

- mínimos cuadrados;
- máxima verosimilitud;
- métodos de optimización;
- métodos bayesianos;
- otras técnicas estadísticas y computacionales.

<br>

### 7. Validación

La **validación** consiste en evaluar si el modelo es capaz de reproducir adecuadamente el comportamiento del sistema en situaciones distintas de aquellas utilizadas para construirlo o calibrarlo.

Esto puede hacerse comparando las predicciones del modelo con datos independientes, observaciones experimentales o comportamientos conocidos.

Una discrepancia entre el modelo y los datos no significa necesariamente que el modelo sea inútil. Puede indicar que debemos revisar:

- los supuestos;
- las variables seleccionadas;
- los parámetros;
- la calidad de los datos;
- la formulación matemática.

<br>

### 8. Refinamiento del modelo

El proceso de modelamiento puede requerir modificar el modelo inicial.

Podemos incorporar nuevas variables, cambiar determinados supuestos, modificar los parámetros o incluso formular un modelo completamente diferente.

Por esta razón, el modelamiento matemático debe entenderse como un proceso de **construcción, análisis, comparación y refinamiento**.

De manera esquemática, podemos representar este proceso como:

<!-- ESPACIO PARA GRÁFICO: Proceso de construcción y refinamiento de un modelo -->

<br><br>

## El rol de la programación científica

La programación científica se ha convertido en una herramienta fundamental para el modelamiento matemático. Permite realizar cálculos numéricos, analizar grandes cantidades de datos, implementar algoritmos, resolver ecuaciones y simular sistemas complejos.

La computadora permite, por ejemplo:

- realizar experimentos numéricos;
- explorar el efecto de los parámetros;
- aproximar soluciones de ecuaciones;
- simular sistemas dinámicos;
- generar realizaciones de modelos estocásticos;
- analizar grandes conjuntos de datos;
- visualizar resultados;
- comparar las predicciones de un modelo con observaciones.

Es importante, sin embargo, distinguir entre el **modelo matemático** y su **implementación computacional**. La computadora ejecuta los procedimientos que hemos definido, pero no sustituye la formulación matemática ni el razonamiento necesario para decidir qué modelo utilizar.

En este curso utilizaremos la programación como una herramienta para explorar y comprender los modelos matemáticos.

<br><br>

## Python y Google Colab

Existen numerosos lenguajes de programación que pueden utilizarse para realizar computación científica. En este curso trabajaremos principalmente con **Python**, debido a su sintaxis relativamente sencilla y al amplio conjunto de herramientas disponibles para cálculo científico, análisis de datos y visualización.

Entre las bibliotecas que utilizaremos se encuentran:

- **NumPy**, para cálculo numérico y manipulación de arreglos;
- **SciPy**, para métodos numéricos, optimización y ecuaciones diferenciales;
- **Pandas**, para manipulación y análisis de datos;
- **Matplotlib**, para visualización de resultados;
- **SymPy**, cuando sea necesario realizar cálculos simbólicos.

Trabajaremos principalmente utilizando **Google Colab**, que permite ejecutar código Python directamente desde el navegador. Esto facilita que los estudiantes puedan reproducir, modificar y experimentar con los ejemplos del libro sin necesidad de instalar localmente un entorno de programación científica.

Los notebooks utilizados durante el curso estarán integrados con el desarrollo de los modelos, de manera que la programación no sea un componente separado, sino una herramienta para **construir, analizar, simular y visualizar modelos matemáticos**.

<br><br>

## ¿Qué estudiaremos en este curso?

A partir de las ideas introducidas en este capítulo, el curso estudiará diferentes familias de modelos matemáticos y las herramientas necesarias para analizarlos.

Comenzaremos con modelos construidos a partir de **datos**, utilizando técnicas de regresión. Posteriormente estudiaremos modelos que describen la **evolución de sistemas discretos**, para luego pasar a modelos de evolución continua mediante ecuaciones diferenciales.

Finalmente, introduciremos modelos **estocásticos**, en los cuales la incertidumbre y la aleatoriedad forman parte explícita de la descripción matemática.

De esta manera, las principales unidades del curso serán:

- **Modelos por regresión:** construcción y ajuste de modelos a partir de datos.
- **Modelos discretos de evolución:** descripción de sistemas que cambian paso a paso.
- **Modelos continuos:** descripción de sistemas cuya evolución se desarrolla continuamente en el tiempo.
- **Modelos estocásticos:** incorporación de incertidumbre y aleatoriedad en los modelos.

A lo largo de todas estas unidades, la **programación en Python y Google Colab** será utilizada como una herramienta para experimentar con los modelos, realizar simulaciones, visualizar resultados y desarrollar intuición matemática.

<br><br>

## Ideas principales

Al finalizar este capítulo, debemos tener presentes algunas ideas fundamentales:

- Un modelo matemático es una **representación simplificada** de un fenómeno.
- La construcción de un modelo depende de la **pregunta que queremos responder**.
- Los modelos utilizan variables, parámetros y relaciones matemáticas para representar un sistema.
- Los modelos pueden ser **deterministas o estocásticos**.
- También pueden ser **discretos o continuos**.
- Estas dos clasificaciones son independientes.
- La construcción de un modelo es un proceso **iterativo** que puede involucrar formulación, análisis, calibración, validación y refinamiento.
- La programación permite **explorar, simular y analizar** modelos matemáticos.
- En este curso utilizaremos **Python y Google Colab** como herramientas computacionales fundamentales.
