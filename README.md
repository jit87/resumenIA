IA - Resumen del temario de la UOC.
===================================

TEMA 1 - Resolución de problemas y búsqueda
----------------------------------------------------------
Coste del recorrido: se calcula sumando el coste de las aristas.

Búsqueda uniforme: tiene en cuenta el coste de las aristas. Es completa y óptima cuando la función del coste siempre es positiva.

Búsqueda ávida: tiene solo en cuenta el heurístico.

Búsqueda A*: tiene en cuenta el coste y el heurístico. Es decir, cada nodo es   [(u, C + H)]. Donde C es la suma acumulada de las aristas hasta llegar al nodo u, y H es H(u). 
El coste del recorrido se calculará igual que en los otros métodos. La solución será óptima si el heurístico es admisible, si no es admisible el algoritmo A* no garantiza que encontremos el óptimo. 

Admisibilidad: dicho de la función heurística que es admisible si nunca sobrestima el coste real,  es decir no sobreestima el coste de alcanzar la meta desde ningún nodo. 
Un heurístico admisible puede ser consistente o no.  Si se sobreestima algún óptimo es no admisible.

Consistencia: para que h sea consistente tiene que ser primero admisible. Un heurístico de un grafo es consistente si es un heurístico admisible con la
 propiedad siguiente: para todo par de nodos de un grafo x e y, si hay un camino del nodo x al nodo y, entonces h(x) ≤ coste(x, y) + h(y), donde coste(x,
 y) corresponde a ir de x a y. Si no da ningún rodeo es consistente el heurístico, es decir no replantea el camino más corto hacia ningún vértice.

Diferencias entre A* completo y A* simplificado:
-  A* completo:  cuando consideramos los sucesores del nodo actual, si encontramos uno que ya está en el conjunto de cerrados, calculamos su coste
 y si mejora el coste que tenía cuando lo cerramos, sacamos el sucesor del conjunto de cerrados y lo volvemos a situar en el conjunto de abiertos con
 el coste revisado. Por tanto:
       Revisa y actualiza el coste de los nodos ya visitados si encuentra un camino mejor (de menor coste).
       Por tanto, reexplora nodos si es necesario para encontrar el camino realmente óptimo.
       Tiene un mayor coste computacional, pero garantiza la solución más corta si h(n) es admisible.
-  A* simplificado: cuando consideramos los sucesores del nodo actual, si encontramos uno que ya está en el conjunto de cerrados, lo ignoramos.
   El A* simplificado solo funciona bien si el heurístico es consistente.
	No actualiza los costes de nodos que ya han sido visitados (cerrados).
	Por tanto, no reexplora nodos aunque exista un camino mejor.
	Es más eficiente en tiempo y memoria, pero puede no encontrar el camino óptimo.



Propiedades de los algoritmos: 
- Completitud: un algoritmo de búsqueda es completo si, cuando un problema tiene solución, este la encuentra.

- Optimalidad: un algoritmo de búsqueda es óptimo cuando en un problema con diferentes soluciones siempre encuentra la solución de más «calidad».

- Complejidad en cuanto al tiempo: el tiempo que tarda el algoritmo en encontrar la solución.

- Complejidad en cuanto al espacio: la memoria que necesita el algoritmo para poder encontrar la solución.

- Algoritmos anytime: un algoritmo de búsqueda es anytime cuando puede encontrar una solución para cualquier asignación de tiempo de computación.



TEMA 2 - Sistemas basados en el conocimiento
----------------------------------------------------------
REGLAS

Estrategias de selección de reglas (para resolver conflictos):
- Orden textual: se seleccionan las reglas por el orden de aparición.
- Recencia: se selecciona la regla más reciente en la memoria de trabajo, requiere una marca de tiempo para cada regla. Se selecciona la regla donde los predicados tienen la última marca de tiempo. Hay que tener en cuenta el tiempo de los átomos.
- Especificidad: se selecciona la regla que corresponde a objetos más específicos (mayor número de conjuntandos, es decir predicados en el antecedente unidos por una conjunción)

Eficiencia de criterios: El menos eficiente es el de recencia, puesto que selecciona en función de la marca de tiempo más reciente (índice de la última iteración finalizada) accediendo a cada elemento que compone el antecedente de cada regla. Si no hay más criterios, todas aquellas reglas que presenten la misma marca de tiempo en alguno de los antecedente estarán empatadas. También se pueden producir empates con el criterio de especificidad.
Por lo tanto, el criterio de orden textual es el más eficiente porque permite resolver conflictos SIEMPRE y con un coste de búsqueda menor que los otros. Es decir, con el orden textual no se producen empates. 

Obstinancia: propiedad que dice que solamente se utiliza cada regla una vez

Encadenamiento (o razonamiento) hacia adelante:  Se dice razonamiento hacia adelante porque lo que miramos para saber si una regla se puede aplicar es si el antecedente se cumple. 
Si se cumple, añadiremos a la memoria de trabajo las conclusiones de la regla. Así, vamos de los antecedentes de las reglas a las conclusiones.
Estudia qué se puede demostrar dada una base de conocimiento y un sistema de reglas.

Encadenamiento (o razonamiento) hacia atrás:  La idea es que aquello que hay en la conclusión será cierto si se cumplen las condiciones que aparecen en el antecedente de una regla. 
Así, para poder demostrar la conclusión, debemos demostrar los antecedentes de las reglas. Estudia a partir de qué reglas se puede demostrar la base de conocimiento.

En el encadenamiento hacia atrás no coinciden la KB (base de conocimiento) con la MT (memoria de trabajo), la KB permanece inmutable. 
En el encadenamiento hacia delante KB=MT, a medida que aumenta la memoria de trabajo se aumenta la KB.

Memoria de trabajo: corresponde a la otra parte del aspecto formal de los sistemas basados en reglas. Se incluyen aquí todos aquellos hechos que pueden ser relevantes para el problema concreto que se quiere resolver. A diferencia del contenido de la base de reglas, aquí la información es temporal y corresponde al problema concreto que se quiere resolver.


MARCOS

Elementos de marcos: 
 
Marcos: Es un sistema de representación del conocimiento, basado en el conocimiento de situaciones anteriores que permite su ajuste a las nuevas situaciones. 
Formalmente, un sistema de marcos es una red donde cada nodo representa un objeto (un concepto o un individuo) y los arcos corresponden a las relaciones que se pueden establecer entre los objetos. Los objetos se representan en marcos, que son un conjunto de campos que lo definen

Procedimiento demonio (en marcos): procedimiento que se llama como efecto secundario de alguna actuación relevante en la base de conocimientos.

Tipos de campos en los marcos: los de miembro y los propios. Los primeros son aquellos campos que se sitúan en cada instancia de un objeto (cada instancia –cada miembro de la clase– posee su propia copia y la modifica libremente), y los segundos son los que son propios del marco (y, por lo tanto, que comparten todas las instancias). El campo propio no se puede modificar al heredarlo, el campo miembro sí.
Los campos pueden almacenar información de tipo muy diferente. Algunos de los elementos que típicamente se pueden incluir son éstos: valores de un dominio cualquiera, referencia a otros marcos, restricciones sobre valores, funciones. 

Subclase: La relación de subclase corresponde a cuando un concepto es un caso particular de otro. 

Superclase: La relación de superclase constituye la relación inversa: cuando un concepto es más general que otro.

Instancia: La relación de instancia la encontramos cuando un marco corresponde a un individuo particular de una clase.

Herencia múltiple: Tenemos herencia múltiple cuando un objeto es instancia de más de una clase, o bien si es subclase de más de una clase. En estos casos, pueden presentarse conflictos para determinar la respuesta del sistema porque según el orden en el que se consideren las relaciones de superclase el sistema retornará una cosa u otra.
Es decir, pueden darse conflictos a la hora de asignar valores al objeto instanciado heredero, para solucionarlos hay que recurrir a los algoritmos de búsqueda. 
Una manera de resolver este problema es mediante un algoritmo de ordenación topológica. Este algoritmo, dado un grafo no cíclico, calcula una lista ordenada de nodos en la que se mantienen las relaciones que existen entre los nodos del grafo. Esta lista es la llamada lista de precedencias. Si las propiedades en conflicto se encuentran en distinto nivel, se elegirá aquel valor de la propiedad que salga antes; si se encuentran en el mismo nivel, el valor elegido dependerá de si recorremos desde la rama derecha o la izquierda.



TEMA 3 - Incertidumbre y razonamiento aproximado
----------------------------------------------------------------

SISTEMAS DIFUSOS

La función trapezoidal tiene cuatro tramos (a,b,c,d).  Los tramos crecientes de la función se escriben como: 
f(x) = x - a / b - a  
siendo a el extremo inferior y b el extremo superior del intervalo (c,d). 
Los tramos decrecientes serán: 
f(x) = d - x / d - c 

Sistemas de inferencia:
 - T-conorma: para operadores OR
 - T-norma: para operadores AND
Cuando varias reglas apuntan al mismo término, el conflicto se resuelve con la T-conorma (porque es como una serie de conectores OR)

Nitidificación:  consiste en obtener un valor nítido a partir de un conjunto difuso. De hecho, existen varias maneras de realizar el proceso de nitidificación. Una de éstas la constituye el llamado centro de masas (o centro de área) y se define como una media de los valores del dominio, cada uno ponderado según su pertenencia al conjunto que estamos nitidificando.


Pasos de construcción de sistema difuso:

   1. Identificación del problema
   	   Se plantea un problema con incertidumbre.
	   Caso: Cocinar una carne según grosor y nivel de cocción deseado, queremos saber el tiempo de cocción necesario.

   2. Definición de variables lingüísticas
    Se determinan las variables de entrada y salida con sus respectivos términos lingüísticos.

         Entrada 1: grosor de la carne  - términos (fina, media, gruesa) ->  F,M,G

         Entrada 2: nivel de cocción deseado - términos (poco hecha, al punto, hecha) -> PH, AP, H

         Salida: tiempo de cocción - términos (corto, medio, largo) -> TC,TM,TL

3. Construcción de funciones de pertenencia
   A cada término lingüístico se le asigna una función de pertenencia (que pueden ser triangular, trapezoidal...).
   Estas funciones permiten representar los grados de pertenencia difusos (entre 0 y 1).

4. Formulación de reglas difusas
   Se emplean reglas lógicas como: Si grosor de carne es "fino" y nivel de cocción es "poco hecho", entonces tiempo es "corto". Esto se formaliza del siguiente modo:
      F ^ PH -> TC

5. Inferencia difusa
   Se aplican las reglas al caso real y se calcula el grado de activación de cada regla mediante  operadores lógicos:

     AND : T-norma

     OR : T-conorma

     (Se activarán aquellos términos del antecedente de cada regla que, en función de las variables de entrada, hayan sido atravesados por la línea vertical que representa el valor de la variable de entrada).

      Si en el consecuente de la regla hay conflicto por tener términos linguisticos activos repetidos y con distinto nivel de activación, se aplica la t-conorma para decidir el nivel de  activación.

     
6. Nitidificación
    Primero se combinan todas las salidas difusas de las reglas activadas. Lo que nos arroja un conjunto de áreas bajo curvas, delimitadas por los niveles de activación finales. 

    Con la nitidificación se transforma el resultado difuso en un valor numérico único.






TEMA 4 - Introducción al aprendizaje computacional
----------------------------------------------------------------
Construcción de un árbol de decisión:
 Un árbol de decisión es un algoritmo de  aprendizaje computacional supervisado que clasifica ejemplos a partir de decisiones sucesivas basadas en los valores de sus atributos. Su  construcción se realiza a partir de un conjunto de entrenamiento que contiene instancias asociadas a clases conocidas.
 El proceso comienza con un conjunto de datos en el que cada instancia está descrita por varios atributos y una clase objetivo. El objetivo es construir un árbol que permita predecir la clase de nuevas instancias desconocidas.
 En cada iteración, se evalúan todos los atributos disponibles para determinar cuál proporciona la mejor partición del conjunto actual. La calidad de una partición se mide mediante la bondad. De modo que se escoge el atributo que maximiza esta medida. Este atributo se convierte en un nodo de  decisión, y se crearán ramas para cada uno de sus valores posibles.
 Cada rama del nodo lleva a una partición. Para cada partición:
 Si todas las instancias tienen la misma clase, se crea un nodo terminal con esa clase.
 Si hay mezcla de clases y aún quedan atributos por evaluar, se sigue iterando.
 La construcción del árbol termina cuando se cumple alguna de estas condiciones:
 Todos los ejemplos en un nodo pertenecen a la misma clase.
 No quedan atributos por dividir.
 Se alcanza una profundidad máxima o un número mínimo de ejemplos por nodo (según configuración).
 Una vez construido, el árbol se usa para clasificar nuevos ejemplos. El proceso consiste en recorrer el árbol desde la raíz, siguiendo las ramas   correspondientes a los valores del ejemplo hasta llegar a un nodo terminal, que contiene la clase predicha.


K-means (k-medias): es un método de clustering (agrupamiento no supervisado) que organiza un conjunto de datos en k grupos o clústeres. Cada observación se asigna al grupo cuyo centroide (es decir, el punto medio o promedio de los datos de ese grupo) se encuentra más próximo. El valor de k determina la cantidad de agrupamientos que se crearán.

El procedimiento básico del algoritmo es el siguiente:

- Seleccionar al azar k centroides iniciales. Estos no tienen que ser necesariamente datos reales, pero sus coordenadas deben estar dentro del rango de los valores.
- Asignar cada elemento del conjunto de datos al centroide más cercano, generando así k grupos.
- Calcular nuevamente los centroides de cada grupo, ubicándolos en la posición promedio de los puntos que lo conforman.
- Repetir los pasos 2 y 3 hasta que las asignaciones de los puntos ya no cambien o hasta alcanzar el número máximo de iteraciones establecido.


KNN (k Nearest Neighbors): es un algoritmo de aprendizaje supervisado que clasifica los datos en diferentes clases en función de la distancia. Es decir, para cada dato nuevo se mide la distancia con respecto a los datos anteriores y se asignará a aquella clase del dato que se encuentre a menos distancia.  K será, en este caso, el número de vecinos cercanos que queremos comprobar para ubicar el dato.


Red neuronal:  es un método de aprendizaje computacional supervisado que se basa en una estructura de nodos interconectada a través de aristas que representan operaciones que se realizan sobre las salidas de los nodos. Emula el comportamiento de las neuronas biológicas. Los nodos reciben unas señales y las trasmiten a otros nodos, en esa transmisión se realizan operaciones que activan o no el siguiente nodo. 
se compone de los elementos siguientes:
 - Una capa de unidades de entrada, que reciben las variables disponibles del exterior para tratar el problema.
 - Una capa de unidades de salida, compuesta por una o más unidades que producen una salida al exterior, que es el «resultado» de la red.
 - Una capa de unidades ocultas, que reciben conexiones de la capa de entrada y se conectan a las unidades de salida.
 - Finalmente, el conjunto de conexiones entre capas. En general, las conexiones entre las unidades son unidireccionales.

Funcion de activación: es una función matemática que determina el cálculo/operación que hace una capa intermediaria de la red neuronal de modo que la salida de esa capa sea una modificación de la señal de entrada.
ReLU por ejemplo es una función de activación, que opera sobre la entrada para que la salida muestre solo numeros positivos. 

ReLu(z) = max(0,z)

Heaviside(z) = { 0  si x < 0 ;  1  si >= 0 

