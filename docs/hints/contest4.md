---
title: contest 4 - hints y códigos de ejemplo
---
[Index](../index) > [Contests](../contests) > [Contest 4](../contests#contest-4) > ```{{page.title}}```

### A - TROY Query
<details> 
  <summary>Hint 1</summary>
  Noten que en vez de pensar en la cantidad de veces que cada fila/columna fue actualizada para llegar a la configuración actual, sólo importa la paridad de estas actualizaciones. Es decir, si fueron updateadas una cantidad par o impar de veces.
</details>
<details> 
  <summary>Hint 2</summary>
  Si una celda es igual en ambos TROYS entonces fue actualizada una cantidad par de veces, sólo hay 2 formas de que esto pase, que su fila y columna respectivas ambas hayan sido actualizadas una cantidad par de veces o que ambas hayan sido actualizadas una cantidad impar de veces (de esta forma la suma es par). De la misma forma, si la celda marca distinto entre los TROYS, la suma debe ser impar, por lo que una debe ser impar y la otra par. Piensen en cómo llevar registro de estas implicancias de forma que sea fácil chequear en caso de una contradicción.
</details>
<details> 
  <summary>Solución + código</summary>
  Podemos registrar las implicancias como conjuntos de un Union Find. Es decir, generamos inicialmente 2 (R + C) conjuntos, dos para cada fila y columna, que representan la posibilidad de que sean par o impar. Cuando vemos el valor de una celda unimos los conjuntos correspondientes según el hint 2, de forma que conceptualmente estamos creando conjuntos de posibles valores que si pasan deben hacerlo juntos para no contradecir los registros. Si en algún momento juntamos a una fila o columna par con su misma fila o columna impar entonces tenemos una contradicción, desde ese momento en adelante la respuesta es siempre "No".
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Codeforces/TROYQuery.cpp">Código de ejemplo</a>
</details>

### D - K12-Bored of Suffixes and Prefixes
<details> 
  <summary>Hint</summary>
  Notemos que si mantenemos la matriz con valores correspondientes al número de cada letra (A: 1, B: 2, ...) en vez de la letra en si, la consulta que se pide es equivalente a simplemente la suma en esa región.
</details>
<details> 
  <summary>Solución + código</summary>
  Podemos mantener registro segun el Hint en un Fenwick Tree 2D. Cada update será realizar N updates a lo largo de la fila/columna correspondiente. Cada consulta será devolver la suma en esa región.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/SPOJ/K12-BoredOfSuffixesAndPrefixes.cpp">Código de ejemplo</a>
</details>

### E - Matrix Summation
<details> 
  <summary>Hint</summary>
  Deben ocupar directamente una de las estructuras explicadas en clase en este problema.
</details>
<details> 
  <summary>Solución + código</summary>
  Basta con ocupar directamente un Fenwick Tree 2D para sumas.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/SPOJ/MatrixSumation.cpp">Código de ejemplo</a>
</details>

### F - UnDetected
<details> 
  <summary>Hint</summary>
  Podemos pensar que el momento en que ya no voy a ser capaz de cruzar el campo es cuando los robots activados cubren completamente el campo en una "linea", es decir separan la mitad inferior de la superior. Deben pensar en una forma de ir actualizando una estructura para cada sensor extra que agreguen de forma de poder detectar cuando se forme una barrera rápidamente.
</details>
<details> 
  <summary>Solución + código</summary>
  Podemos pensar en N + 2 conjuntos en un Union Find, uno por cada sensor y uno para el lado izquierdo y derecho del campo. Cada vez que activamos un sensor verificamos si choca con alguno de los lados o con alguno de los sensores activos, en caso de hacerlo unimos los conjuntos correspondientes. Si en algún momento el conjunto correspondiente al borde izquierdo y al derecho son unidos, sabemos que se formó una barrera y ya no se podrá cruzar.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Kattis/UnDetected.cpp">Código de ejemplo</a>
</details>

### H - Cut Inequality Down
<details> 
  <summary>Hint 1</summary>
  Piensen en una forma de procesar las queries en orden de tal forma que con realizar sólo una pasada por cada momento temporal podamos tener la respuesta a todas las queries.
</details>
<details> 
  <summary>Hint 2</summary>
  Una opción es ir avanzando el tiempo desde el primer mes hasta el último procesando cuando corresponda distintos eventos. Estos pueden ser, el inicio de una query (con su monto inicial), y el fin de una query, donde guardamos el valor actual que tiene la query en ese momento. Debemos poder llevar cuenta del valor luego de las perdidas/ganancias en cada mes, sin pasarnos de los límites.
</details>
<details> 
  <summary>Hint 3</summary>
  Notemos que es muy ineficiente ir sumando la ganancia / pérdida de cada mes a cada query activa, esa solución es cuadrática y no pasa en tiempo, por lo que debemos optimizarla. Una opción es en vez de sumar a cada una, mantener una variable de offset que me guarde las ganancias acumuladas hasta el momento actual, luego el valor que tengo guardado más el offset sería el verdadero valor de la query. Sin embargo también debemos ser capaces de ajustar cuando los valores de las queries activas se pasen de los límites superior o inferior. Una forma de hacer esto es mantener los valores de las queries en un set ordenado, mientras el valor más grande se pase del límite superior, sacamos del set, ajustamos y volvemos a insertar, similar en el límite inferior. Notemos que aún hay problemas de tiempo en esta solución, pues en el peor caso cada query activa se pasa de los límites en cada tiempo, piensen en una forma de no tener que modificar tantas veces el set.
</details>
<details> 
<summary>Hint 4</summary>
  Una opción para arreglar el problema que se evidenció al final del hint 3 es usar un Union Find, de tal forma de sólo guardar en el set un representante de cada conjunto del Union Find. Inicialmente podemos tener tantos conjuntos como Queries, sim embargo cuando sacamos cosas del set que se pasen del límite inferior, sabemos que van a tener el mismo valor de ahí en adelante, por lo tanto nos basta con volver a ingresar sólo uno de los que se hayan pasado, unir los conjuntos en el Union Find y al final de una query se guarda el valor que tiene el índice del padre de la query en el union find. Esto mejora la complejidad pues a lo más se unen una cantidad igual a la cantidad de queries.
</details>
<details> 
  <summary>Solución + código</summary>
  La solución consiste en implementar todas las ideas de los hints. Podemos implementar el orden de las queries en una priority_queue donde ordeno los inicios y términos de queries. Mantendo en cada momento un set de pares ordenados con el valor de cada query activa y su índice, juntamos según el hint 3 si se pasan en algún momento y retorno según corresponda.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Matcomgrader/CutInequalityDown2.cpp">Código de ejemplo</a>
</details>

<!-- <details> 
  <summary>Hint</summary>   
</details>
<details> 
  <summary>Solución + código</summary>
  <a href="">Código de ejemplo</a>
</details> -->

[Index](../index) > [Contests](../contests) > [Contest 4](../contests#contest-4) > ```{{page.title}}```
