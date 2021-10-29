---
title: contest 8 - hints y códigos de ejemplo
---

[Index](../index) > [Contests](../contests) > [Contest 8](../contests#contest-8) > ```{{page.title}}```

### A - Dividing the names
<details> 
  <summary>Hint 1</summary>
  Notar que la respuesta es igual a la suma de los largos abreviados x N. Por lo tanto, basta resolver el problema de separar los nombres de tal manera que la suma de los largos abreviados sea la mínima posible, y luego multiplicamos el resultado por N.
</details>
<details> 
  <summary>Hint 2</summary>
  La información de todos los nombres se puede comprimir en un trie. Piensa en cómo aprovchar el trie para encontrar la repartición óptima de los nombres entre calles y avenidas. Un hint clave: si tenemos varias palabras que pasan por el mismo nodo del trie, sólo podemos abreviar si es que mandamos una palabra a las calles y el resto a las avenidas o viceversa. Si mandamos dos o más a cada grupo, no podemos abreviar.
</details>
<details> 
  <summary>Solución + código</summary>
  La solución es hacer un backtracking + memoization sobre un trie (o en otras palabras, un DP sobre el trie). Los nodos de nuesro trie van a tener un contador count[nodo] que nos dice cuántas palabras pasaron por ese nodo cuando armamos el trie. Entonces nuestra función será DP(nodo, n) = la mínima suma de largos de los sufijos que parten desde este nodo, sujeto a que debemos mandar n sufijos a las calles y (count[nodo] - n) sufijos a las avenidas. La respuesta al problema original entonces está dada por DP(0, N), ya que 0 es la raíz, los sufijos que parten en la raíz son las palabras originales y debemos mandar N a las calles y el resto a las avenidas. La gran dificultad del problema queda entonces en la recurrencia. Si estamos resolviendo DP(nodo, n), supongamos que nodo tiene k hijos. Entonces el n lo tenemos que repartir entre los k hijos, es decir, tenemos que escoger n1, n2, ..., nk tales ques n1 + n2 + ... + nk = n, y resolver recursivamente DP(hijo_i, n_i). La forma de probar todos los posibles n1, n2, ..., nk se puede hacer con una función recursiva que por cada nodo hijo prueba todos los valores válidos con un for y luego llama recursivamente a la misma función para el siguiente hijo, y así sucesivamente. Ahora, con respecto a la respuesta misma, si estamos resolviendo DP(nodo, n), hay count[nodo] palabras que pasaron por nodo. Es decir, nodo contribuye con count[nodo] caracteres a la respuesta final, EXCEPTO si es que podemos aplicar abreviaciones. ¿Cuándo podemos abreviar? Si n == 1, podemos restar 1 a la respuesta ya que esta palabra está sola y se puede abreviar. Si el resto (count[nodo] - n) == 1, también se puede restar 1 a la respuesta ya que esta palabra está sola y se puede abreviar. <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/LiveArchive/6824_DividingTheNames.cpp">Código de ejemplo</a>
</details>

### B - Queries for Number of Palindromes
<details> 
  <summary>Hint 1</summary>
  Dado el tamaño del string podemos preprocesar todos los substrings cuadráticamente para saber cuáles conforman palíndromos, esto puede ser chequeado con Rolling Hashing hacia ambos lados por ejemplo. Piensen en cómo usar este preprocesamiento para obtener la solución.
</details>
<details> 
  <summary>Hint 2</summary>
  Dados l y r, la cantidad de substrings en [l, r] es la cantidad en [l, r - 1] más la en [l + 1, r] menos la en [l + 1, r - 1] más 1 si el mismo substring [l, r] era un palíndromo.
</details>
<details> 
  <summary>Solución + código</summary>
  Usando los hints anteriores se puede armar un algoritmo de programación dinámica que cuente los substrings que son palíndromos para cada l y r usando la recursión del hint 2.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Codeforces/QueriesForNumberOfPalindromes.cpp">Código de ejemplo</a>
</details>

### C - Efficient managing
<details> 
  <summary>Hint 1</summary>
  Primero notemos que el grafo descrito corresponde a un árbol. En ese caso podemos precalcular el precio de viajar desde un nodo raíz a cualquiera de los otros nodos en tiempo lineal con un dfs. Basta hacer un dfs que acumule el xor de las aristas usadas, pues el xor de los valores sólo tiene aquellas potencias de 2 con apariciones impares.
</details>
<details> 
  <summary>Hint 2</summary>
  Notemos que si estamos analizando el nodo i, cualquier camino desde i se puede ver como parte del subárbol de i en el arbol con la raíz original o puede ser un camino que sube y luego baja por el árbol, en ambos casos, cualquier camino que salga de i tendrá un costo igual al xor del camino precalculado desde la raíz hasta i xor con el precalculado de la raíz al nodo final del camino tomado desde i. Luego el problema puede ser reformulado a precalcular como el hint 1 y para cada i encontrar cual de los valores precalculados genera un mayor xor al ser combinados con el precalculado para i.
</details>
<details> 
  <summary>Hint 3</summary>
  Finalmente noten que cada uno de los valores precalculados puede ser cisto como un string binario, para encontrar el que genera el mayor xor con otro de estos strings, digamos x, se puede tomar un approach greedy que va condicionando tomar aquellos números con bits más grandes que difieran a los de x. Para esto piensen en qué estructura les deja ordenar los strings por los valores separando cada vez que difieren.
</details>
<details> 
  <summary>Solución + código</summary>
  La solución corresponde a usar la reducción de los hints 1 y 2 y hacer un Trie de los strings binarios descritos en el hint 3. El Trie recibirá los valores precalculados en forma binaria pero los ingresará al Trie con los bits más grandes al principio. Esto pues podemos encontrar el mayor xor posible con los números guardados con respecto a un número x usando un approach greedy que elija bits distintos siempre que se pueda en el trie (analizando desde bits más grandes a menos igual que como fueron ingresados).
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/SPOJ/EfficientManaging.cpp">Código de ejemplo</a>
</details>


### D - Death Stars (medium)
<details> 
  <summary>Hint</summary>
  Piensa en una forma de acelerar la comparación entre strings.
</details>
<details> 
  <summary>Solución + código</summary>
  Usamos rolling hashing. Creamos una instancia de la clase hash por cada fila de la matriz vertical y por cada fila de la matriz horizontal. Luego hacemos un doble for y en cada caso con un tercer for hacemos M comparaciones aprovechando los hashes para ver si las submatrices de MxM coinciden. Para hacer el código más rápido, hacemos break del tercer for apenas algo no coincida. <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/Codeforces/958A2_DeathStars(medium).cpp">Código de ejemplo</a>
</details>

### E - Diccionário Portuñol
<details> 
  <summary>Hint 1</summary>
  Podemos pensar el problema como descontar de la cantidad de combinaciones totales todos los que se repitan.
</details>
<details> 
  <summary>Hint 2</summary>
  Para contar las totales podemos contar cada prefijo en portugués posible usando un Trie de las palabras en portugúes, y para la cantidad de sufijos en español podemos usar un Trie de las palabras en español reversas (así no repetimos sufijos). Luego la cantidad de nodos usados en cada trie multiplicados es la cantidad total de combinaciones prefijo sufijo posibles. Sólo queda descontar las que se repitan.
</details>
<details> 
  <summary>Hint 3</summary>
  La única forma de que estemos contando combinaciones repetidas es que haya un prefijo en portugúes que termine con la misma letra que empieza un sufijo en español, así se podría tomar esa letra indistíntamente de ambos lados. Podemos precaluclar cuantos prefijos portugueses terminan en cada letra fácilmente usando un dfs sobre los nodos del trie. Lo mismo para las primeras letras de los sufijos en español.
</details>
<details> 
  <summary>Solución + código</summary>
  La solución consiste en descontar de lo contado según hint 1 las repeticiones como mencionadas en el hint 2. Para contarlas hacemos 2 dfs, uno que cuente prefijos en portugués terminados en cada letra (prefijos de largo mayor a 1 pues no puede ser vacío según enunciado y estamos contando repeticiones donde tomamos o no la última letra). En el otro dfs cada vez que encontramos un sufijo que empieze en una letra, descontamos de la respuesta la cantidad de prefijos que terminaban en ella.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/UVA/DiccionarioPortunol.cpp">Código de ejemplo</a>
</details>


### F - Cellphone Typing
<details> 
  <summary>Hint</summary>
  Si comprimimos todo en un trie, ¿se te ocurre una forma fácil de resolver el problema?
</details>
<details> 
  <summary>Solución + código</summary>
  Metemos todas las palabras en un trie, y en cada nodo contamos la frecuencia de palabras que pasaron por ese nodo. Luego, simulamos el proceso de tipear cada palabra navegando el trie desde la raíz y usando los caracteres de la palabra como las instrucciones de navegación. Partimos sumando 1 porque el primer caracter siempre se tipea. Luego, los siguientes caracteres se autocompletan si y sólo si la transición en el trie es obligada (si el nodo anterior solo tiene un puro hijo), esto se puede chequear comparando los contadores, si son iguales no hay bifurcaciones. Al final dividimos la suma total por la cantidad de palabras. <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/LiveArchive/6133_CellphoneTyping.cpp">Código de ejemplo</a>
</details>

### G - Dr. Evil Underscores
<details> 
  <summary>Hint</summary>
  Piensa que los números son strings de largo 30 en binario y con padding de 0's por la derecha de ser necesario. Piensa ahora que los metes en un trie. ¿Se te ocurre cómo resolver el problema?
</details>
<details> 
  <summary>Solución + código</summary>
  Armamos un trie con los números como lo sugiere el hint. Luego podemos encontrar el mínimo xor con un DFS sobre el trie desde la raíz. El DFS va a calcular el mínimo xor posible desde el nodo u. Si u tiene un puro hijo, entonces siempre podemos escoger el mismo bit para que en el xor nos de 0. Si u tienes dos hijos, entonces independiente de cuál bit escogamos, en el máximo siempre va a convenir escoger la rama con el bit opuesto, entonces siempre va a haber un bit prendido en la i-ésima posición (donde i es la profundidad del nodo u) y luego escogemos el mínimo entre los dos DFS's de los hijos. <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/Codeforces/1285D_Dr.EvilUnderscores.cpp">Código de ejemplo</a>
</details>

### H - Isomorphic Inversion
<details> 
  <summary>Hint</summary>
  Piensen en una forma greedy de seleccionar los segmentos.
</details>
<details> 
  <summary>Solución + código</summary>
  Podemos armar los segmentos de forma greedy chequenando con k de 1 creciente separando los primeros y últimos k cada vez que el sustring de los primeros k que quedan sea igual al de los últimos k. Para chequear esto se puede usar hashing preprocesado de todo el string. la respuesta será cuantas veces se pudo separar * 2 más uno si sobraron cosas al medio.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Kattis/IsomorphicInversion.cpp">Código de ejemplo</a>
</details>

<!-- <details> 
  <summary>Hint</summary>   
</details>
<details> 
  <summary>Solución + código</summary>
  <a href="">Código de ejemplo</a>
</details> -->

[Index](../index) > [Contests](../contests) > [Contest 8](../contests#contest-8) > ```{{page.title}}```
