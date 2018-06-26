# trabajoFinal


## Algoritmo seleccionado:

Linear regression.


### Explicación del algoritmo:

La regresión lineal es una técnica que permite modelar la relación entre una variable dependiente y una o muchas independientes.
Su objetivo es la obtención de un modelo que se aproxime lo máximo posible a los valores originales de la variable de salida, entonces, el algoritmo se usa para predecir valores a entradas desconocidas una vez se complete el entrenamiento.
La ecuación matemática en la que se apoya este método es la de las líneas rectas, donde se multiplica un coeficiente por cada variable independiente y se adiciona un factor de error (y = m1*x1 + m2*x2 + b).
Esta fórmula es sencilla, pero permite describir de manera acertada fenómenos lineales, siendo esta misma la restricción del algoritmo.

Entonces, el proceso de entrenamiento o generación del modelo consiste en calcular los coeficientes que se multiplican por cada variable independiente a partir de una colección de datos de entrada y salida conocidos, lo cual originará la ecuación completa para poder calcular posteriormente los valores de salida ante entradas desconocidas.

De acuerdo a la teoría, la evaluación del grado de acierto del modelo se realiza calculando residuos, que es la diferencia entre los valores de referencia y los calculados a partir del modelo.


## Implementación en paralelo del algoritmo:

El paso inicial es cargar los datos para entrenamiento, con los cuales se construye una matriz. Ésta cuenta con una columna donde están los valores de las variables independientes y otra columna con los valores de la variable dependiente.
El siguiente paso es llamar a la función de generación del modelo con los datos cargados previamente, en donde se especifica un número de iteraciones.
De acuerdo a la cantidad seleccionada y el número de máquinas o núcleos disponibles, Spark debería calcular la cantidad de iteraciones que ejecutará cada worker, y delega la administración de los mismos a un máster.
En cada iteración, se genera un grupo de coeficientes determinado, y se procede a calcular el error entre la salida con la ecuación generada y las salidas reales, y como el objetivo del algoritmo es minizar este error, al final del cálculo de todas las iteraciones, el máster recolecta los resultados de cada una de ellas y selecciona la solución con el menor error.

El procedimiento descrito anteriormente es similar al proceso Map-Reduce, donde el cálculo de los coeficientes se llevaría a cabo en la etapa Map, y la selección de la solución con el mínimo error en Reduce.


## Instrucciones de ejecución:

El sistema operativo del computador en el que se desarrolló el trabajo es Ubuntu 16.04.
La configuración del entorno de trabajo se llevó a cabo con la ayuda del siguiente tutorial https://blog.sicara.com/get-started-pyspark-jupyter-guide-tutorial-ae2fe84f594f
Una vez preparado el equipo, se logró ejecutar Jupyter para realizar operaciones con Spark.

El tutorial seleccionado para la parte práctica del ejercicio está disponible en el siguiente enlace https://towardsdatascience.com/building-a-linear-regression-with-pyspark-and-mllib-d065c3ba246a
Los datos del problema propuesto contienen registros que describen diferentes estadísticas relacionadas con vivendas en la ciudad de Boston.
Por ejemplo, hay una columna llamada "crim", que contiene la tasa de criminalidad en la zona, o la columna "chas", que puede valer 1 ó 0 según si la casa está cerca del río de la ciudad, o la columna "rm", que corresponde al número promedio de habitaciones por casa en una zona. Inclusive, hay una columna llamada "black", que indica la proporción de población de raza negra cerca de la casa.
Todas las anteriores y más, son columnas que representan variables de entrada, pero los valores de la variable objetivo son los que se encuentran en la columna "medv", que representa el valor medio de las viviendas ocupadas por sus propietarios en miles de dólares.
La idea es que se genere un modelo que permita predecir el valor medio de una vivienda en la ciudad.

El conjunto de datos usados para el entrenamiento y las pruebas se incluye en el repositorio con el nombre train.csv.
