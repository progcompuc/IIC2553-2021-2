---
title: contest 6 - hints y códigos de ejemplo
---

[Index](../index) > [Contests](../contests) > [Contest 6](../contests#contest-6) > ```{{page.title}}```

### A - Leaders
<details> 
  <summary>Hint 1</summary>
  Notemos que de ser posible ir de un nodo a otro, para que haya un camino simple de largo impar podemos o ir directo pasando por una cantidad impar de aristas o pasar por una componente biconexa con un ciclo impar (la segunda opción siempre tendrá un camino simple que cumpla lo pedido). Si en el camino entre u y v se pasa por una componente biconexa con un ciclo impar la respuesta será siempre positiva, de lo contrario basta con bicolorear el grafo y ver si u y v son de colores distintos.
</details>
<details> 
  <summary>Hint 2</summary>
  Para encontrar componentes biconexas con ciclo impar basta ocupar el mismo dfs que encuentra las componentes pero ir bicoloreando y recordando si los backedges iban a un nodo del mismo color o no, de hacerlo marcan un ciclo impar y al removerlas la componente tiene un ciclo impar.
</details>
<details> 
  <summary>Solución + código</summary>
  La solución consiste en buscar bicomponentes con ciclos de largo impar y removerlas del grafo. Si dos nodos estaban conexos previo a la remoción y después no, es porque su camino pasaba por una de estas componentes por lo que la respuesta será "Yes". En caso de seguir conectadas la respuesta dependerá de si son del mismo color o no.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Codeforces/Leaders.cpp">Código de ejemplo</a>
</details>

### B - Checkposts
<details> 
  <summary>Hint</summary>
  Si es posible ir a un nodo y volver, entonces ambos deben pertenecer a la misma componente fuertmenete conexa.
</details>
<details>
  <summary>Solución + código</summary>
  Basta con encontrar las componentes fuertemente conexas y calcular lo pedido usando las inesecciones de meno costo en cada una. El costo final será la suma de los menores costo y las formas de hacerlo será la multiplicación de cuantas intersecciones tenían ese menor costo en cada componente.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Codeforces/Checkposts.cpp">Código de ejemplo</a>
</details>

### C - Good Travels
<details> 
  <summary>Hint</summary>
  Notemos que si en el camino óptimo que buscamos se pasa por un nodo u, siempre será posible pasar por todos los nodos en la misma componente fuertemente conexa que u. De esta forma podemos como primer paso reducir el grafo original a un grafo alterno donde cada nodo corresponde a una componente fuertemente conexa en el grafo original y sólo nos quedamos con aristas que vayan de una componente a otra. Podemos asignar valor de diversión (fun) de cada componente como la suma de la diversión de los nodos que la componen.
</details>
<details> 
  <summary>Solución + código</summary>
  Haciendo uso del hint, es conocido que el grafo resultante debe ser un DAG (directed acyclic graph). Luego podemos obtener la respuesta pedida usandoi un DP sobre el grafo construido, donde devolvemos la maxima suma de diversiones en un camino de componentes que termine en la componente que corresponda a la ciudad de destino.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/SPOJ/GoodTravels.cpp">Código de ejemplo</a>
</details>

### D - Hegde Mazes
<details> 
  <summary>Hint</summary>
  Si sólo existe un camino simple que une S y T entonces removiendo cualquier arista en el camino los nodos S y T quedarán desconectados, es decir, todas las aristas del camino que buscamos deben ser aristas de corte.
</details>
<details> 
  <summary>Solución + código</summary>
  Basta saber si existe un camino entre S y T que use sólo aristas de corte, para esto podemos usar Union Find uniendo dos nodos si hay una arista de corte entre ellos. Luego la respuesta es si los nodos estan unidos en el union find o no.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/URI/HedgeMazes.cpp">Código de ejemplo</a>
</details>

### E - Necklace
<details> 
  <summary>Hint</summary>
  Siempre que haya un camino donde todas las aristas no sean de corte, se podrá construir un necklace, esto pues al no ser de corte existe otro camino que completa el ciclo para cada arista.
</details>
<details> 
  <summary>Solución + código</summary>
  Basta con encontrar y remover las aristas de corte y ver si después de ese proceso aún hay un camino entre S y T.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/ICPC/Necklace.cpp">Código de ejemplo</a>
</details>

### F - Capital City
<details> 
  <summary>Hint</summary>
  Notemos que si una ciudad es candidata a ser capital, todas las ciudades en la misma componente fuertemente conexa deben serlo, luego basta con saber si alguna de las ciudades en cada componente fuertemente conexa puede ser capital.
</details>
<details> 
  <summary>Solución + código</summary>
  Para chequear si una ciudad puede ser capital basta correr un DFS desde la cuidad en el grafo con las aristas invertidas, si se puede llegar a todos los nodos es porque todos podían llegar a ella por lo que puede ser capital.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/SPOJ/CapitalCity.cpp">Código de ejemplo</a>
</details>

### G - Submerging Islands
<details> 
  <summary>Hint</summary>
  Problema directo de contar puntos de articulación en el grafo
</details>
<details> 
  <summary>Solución + código</summary>
  Ojo, usen un set para contar cuantos hay, si aumentan una variable contarán repetido.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/SPOJ/SubmergingIslands.cpp">Código de ejemplo</a>
</details>

### H - Jobbery
<details> 
  <summary>Hint 1</summary>
  Notemos que si construimos el grafo dirigido que modela las relaciones, si una persona es peligrosa, todas las personas en su misma componente fuertemente conexa también serán peligrosas, pues pueden llegar a la primera persona y por tanto a todas las que él llega.
</details>
<details> 
  <summary>Hint 2</summary>
  Podriamos buscar las componentes fuertemente conexas y correr un dfs que cuente el alcance de cada una, pero esto no pasaría en tiempo. Pensemos en una forma de sólo hacer un dfs de conteo. Noten que siempre la primera componente fuertemente conexa que se encuentra con Tarjan será la más profunda en ese árbol de exploración. Además podemos notar que la componente que buscamos es la menos profunda en el grafo.
</details>
<details>
  <summary>Solución + código</summary>
   Usando los hints podemos ver que podemos aprovecharnos de la naturaleza del agloritmo de tarjan y buscar las componentes en el grafo inverso, de esta forma la primera que encontremos es la única candidata a contener a las personas peligrosas (pues es la más profunda del grafo inverso y por lo tanto la menos del grafo original). una vez encontrada corremos un dfs de conteo en el grafo normal y dejamos de buscar más componentes. si se contó que la componente llegaba a todo el grafo, devolvemos a sus miembros como respuesta.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Timus/Jobbery.cpp">Código de ejemplo</a>
</details>

<!-- <details> 
  <summary>Hint</summary>   
</details>
<details> 
  <summary>Solución + código</summary>
  <a href="">Código de ejemplo</a>
</details> -->

[Index](../index) > [Contests](../contests) > [Contest 6](../contests#contest-6) > ```{{page.title}}```
