---
title: contest 9 - hints y códigos de ejemplo
---

[Index](../index) > [Contests](../contests) > [Contest 9](../contests#contest-9) > ```{{page.title}}```

### A - String Similarity
<details> 
  <summary>Hint</summary>
  Noten que si calulamos el suffix array con arreglo lcp del string original ya se tiene calculado el tamaño de los longuest common preffix de sufijos continuos en el suffix array. Piensen en cómo ocupar esto para obtener la respuesta.
</details>
<details> 
  <summary>Solución + código</summary>
  Podemos buscar el lugar donde está el string completo en el suffix array (buscar la posición del 0). Luego la respuesta será la suma de acumular mínimos hacia derecha e izquierda del arreglo lcp, esto pues el largo común de un segmento continuo del suffix array corresponde al mínimo de los lcp del rango.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/HackerRank/StringSimilarity.cpp">Código de ejemplo</a>
</details>

### B - Match & Catch
<details> 
  <summary>Hint</summary>  
  Piensen en cómo se puede responder lo pedido usando el precálculo de un suffix array y lcp. Noten que todo substring es un prefijo de un sufijo, y para que sea único en el string original basta con que sea de largo mayor al lcp anterior y posterior (pues no habrá otro prefijo de sufijo igual de ese largo).
</details>
<details> 
  <summary>Solución + código</summary>
  Podemos usar el hint 1 pero precalculando sobre el string S1#S2, así podemos filtrar los substrings comunes y unicos de ambos mirando el lcp, de forma que serán continuos en el suffix array pero los lcp inmediatamente posterior y anterior serán menores. Es decir, si estamos en la posición i del suffix array, donde sa[i] es parte de S1 y sa[i + 1] es parte de S2. luego el menor substring común asociado a esa posición debe ser de largo menor o igual a lcp[i], pero sólo será unico en ambos strings si lcp[i] >= largo > max(lcp[i - 1], lcp[i + 1]). Luego si es posible tomamos largo = max(lcp[i - 1], lcp[i + 1]) + 1, y nos quedamos con el menor de estos largos.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Codeforces/MatchAndCatch.cpp">Código de ejemplo</a>
</details>

### C - Gluing Pictures
<details> 
  <summary>Hint 1</summary>
  Noten que basta usar un approach greedy donde vamos completando la palabra buscado usar substrings lo más grandes posibles del string grande. Esto siempre será óptimo, sólo queda saber cómo buscar el mayor substring que podemos tomar de forma eficiente.
</details>
<details> 
  <summary>Hint 2</summary>
  Podemos buscar lo descrito en el hint 1 letra por letra. Dado que hayamos precalculado el suffix array del string original, en este tendremos ordenados los sufijos. Todo substring debe ser el prefijo de un sufijo, luego basta buscar el sufijo que tenga un prefijo común más grande. Piensen cómo hacerlo letra por letra usando búsqueda binaria.
</details>
<details> 
  <summary>Solución + código</summary>
  Podemos buscar letra por letra con búsqueda binaria, inicialmente l = 0, r = N y tenemos todos los sufijos, hacemos búsqueda binaria por una letra y podemos reducir el rango a l', r' donde todos los sufijos en [l', r') comparten la primera letra con el string buscado, luego acotamos este nuevo rango según la segunda letra y así sucesivamente. En el momento donde no podamos encontrar una letra habremos encontrado el substring más largo posible, agregamos uno a la respuesta y empezamos de nuevo del rango [0, N) con la letra que quedamos.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Matcomgrader/GluingPictures.cpp">Código de ejemplo</a>
</details>

### D - Marblecoin
<details> 
  <summary>Hint 1</summary>
  Notar que el impuesto a pagar se puede pensar como un número en base 365. Por lo tanto, nos conviene que los dígitos más significativos sean lo más chicos posibles. Esto implica que nos conviene escoger el tope de stack más chico. ¿Pero qué pasa si hay empate?
</details>
<details> 
  <summary>Hint 2</summary>
  Si hay empates, entonces nos convendría desempatar escogiendo el tope de stack que deja debajo suyo el número más chico. Si hay empate de nuevo, el que debajo el número más chico, y así sucesivamente. ¿Qué pasa si 2 stacks empatan en todo pero uno se acaba antes que el otro (en otras palabras, qué pasa si un stack es prefijo de otro)?
</details>
<details> 
  <summary>Hint 3</summary>
  Si un stack es prefijo de otro, nos conviene priorizar el stack más largo, ya que ese stack a largo plazo nos da más opciones para escoger (en ningún caso es peor escoger el más largo, o da lo mismo o nos conviene).
</details>
<details> 
  <summary>Hint 4</summary>
  Piensa en alguna estructura de datos para hacer comparaciones lexicográficas eficientes entre stacks.
</details>
<details> 
  <summary>Solución + código</summary>
  Concatenamos todos los stacks en un puro string, poniendo como caracter separador y al final el 301 (o cualquier otro valor que sea mayor estricto a todos los caracteres). Luego construimos un suffix array sobre dicho string. De esta manera, el arreglo rank del suffix array nos permite comparar en O(1) los sufijos de dos stacks desempatando de la forma en que nos interesa segúns los hints (notar que el 301 es clave para priorizar stacks más largos). Luego, el problema se reducen simular el proceso de ir sacando topes de stacks, lo cual podemos hacerlo con una priority_queue donde priorizamos los topes de stacks con rank más bajos, y al sacar un tope de stack metemos el tope que queda debajo. <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/LiveArchive/8200_Marblecoin.cpp">Código de ejemplo</a>
</details>

### E - Prefixes and Suffixes
<details> 
  <summary>Hint 1</summary>
  En este problema sirve usar suffix array y el arreglo LCP (longest common prefix). En particular, piensa en un prefijo que también es sufijo y además aparece varias veces más como substring. Los respectivos sufijos aparecen todos juntitos en el suffix array. Además, si miramos los valores del arreglo LCP se pueden ver como las columnas de un histograma, notaremos que el largo del substring corresponde a la altura de la columna más baja en el rango, y que las columnas a las izquierda y a la derecha del rango son altura estrictamente menor.
</details>
<details> 
  <summary>Hint 2</summary>
  Del hint 1, podemos inferir una estrategia: vemos al arreglo LCP como histograma y buscamos rangos de columnas donde una columan en particular es la altura mínima (el largo del substring), todas las demás son >= a ese rango, y las columnas antes y después del rango son de altura menor estricta. Luego bastaría verificar que entre los sufijos del rango se encuentren el sufijo 0 (prefijo) y un sufijo de largo igual a la columna más baja del rango.
</details>
<details> 
  <summary>Solución + código</summary>
  Generamos un suffix array + LCP a partir del string de input. Luego encontramos los rangos maximales de columnas en el arreglo LCP que se mencionó en los hints. Para ello, la idea es fijar la columna i-ésima como la más baja, y luego encontrar los extremos L[i] y R[i] del correspondiente rango de columnas. Este se puede hacer en O(N) con dos pasadas lineales + un stack (descubrir/googlear como resolver linealmente este problema: <https://www.spoj.com/problems/HISTOGRA>). Luego, necesitamos saber el primer y último sufijo en cada rango. Esto se puede hacer en O(1) usando dos sparse tables para obtener el mínimo y máximo por rango. Luego basta verificar si el mínimo es 0 y el máximo + LCP[i] es N. Para evitar duplicados, recolectamos los pares en un set de pares (que de paso nos ordena los pares gratis), y además agregamos el par que siempre va: (N, 1). Finalmente, imprimimos los pares. <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/Codeforces/432D_PrefixesAndSuffixes.cpp">Código de ejemplo</a>
</details>

### F - Lucky Common Subsequence
<details> 
  <summary>Hint</summary>
  Noten que si no existiera el virus, el problema de encontrar la mayor subsecuencia común se puede resolver usando un dp cuadrático con estados i, j, correspondientes a las posiciones que estamos revisando de cada string, luego la recursión es en (i, j) considerar dp(i + 1, j), dp(i, j + 1) y si S1[i] == S[j] considerar 1 + dp(i + 1, j + 1) (retornando el máximo). La respuesta es dp(0, 0). Piensen en cómo adaptar esta recursión para detectar cuando se complete un virus y evitarlo.
</details>
<details> 
  <summary>Solución + código</summary>
  Podemos usar un approach como KMP, en este algoritmo se recorre un string linealmente y se puede detectar cuando aparece otro string dentro, podemos usar este mismo método para detectar si con las letras que se han usado (cuando se pasó a (i + 1, j + 1) en la recursión) se arma el virus. Basta agregar un estado extra al dp que haga referencia al índice del arreglo lps actual.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Codeforces/LuckyCommonSubsequence.cpp">Código de ejemplo</a>
</details>

### G - String Tale
<details> 
  <summary>Hint</summary>
  Hay una solución trivial con KMP.
</details>
<details> 
  <summary>Solución + código</summary>
  Concatena el primer string dos veces, busca la primera aparición del segundo string en el primer string usando KMP. Luego calcular el shift es trivial. <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/acm.timus.ru/1423_StringTale.cpp">Código de ejemplo</a>
</details>

### H - File Retrieval
<details> 
  <summary>Hint 1</summary>
  <p>Supongamos que tenemos varios archivos y tipeamos una query Q = "blabla", y nos aparece una lista de todos los matches de "blabla" en todos los archivos en la forma de pares (File ID, Match Index). Todos esos matches son posiciones donde "blabla" es un substring de un archivo, o en otras palabras, "blabla" es prefijo de un sufijo de algún archivo. Ahora, supongamos que juntamos todos los sufijos de todos los archivos, los metemos a una lista y los ordenamos lexicográficamente: ¿Cómo se ven los matches ahora?</p>
  <p>**SPOILER: todos los sufijos donde "blabla" es prefijo aparecen juntos en la lista (un segmento contiguo de la lista) </p>
</details>
<details>
  <summary>Hint 2</summary>
  Concatenemos todos los archivos en un string largo usando caracteres separadores especiales, y construyamos un <strong>Suffix Array</strong> sobre el string. Construyamos el arreglo <strong>LCP (longest common prefix)</strong> también. Ahora volvamos al ejemplo de la query "blabla". El rango contiguo donde "blabla" hace match es un intervalo maximal de sufijos consecutivos donde todos tienen como prefijo "blabla". Supongamos que este intervalo es [L, R]. Esto implica que LCP[i] >= len("blabla") para i = L, L+1, ..., R-1, y además LCP[L-1] < len("blabla") y LCP[R] < len("blabla"). Notar que el intervalo [L,R] generado por la query Q = "blabla" es equivalente al intervalo generado por query Q' = ("blabla" + algun_extra) que se obtiene alargando Q por la derecha tal que len(Q') = min { LCP[i] para i = L, ..., R-1 }. Si visualizamos el arreglo LCP como un histograma, Q hace match con un rectángulo horizontalmente maximal, y Q' es básicamente aumentar la altura de dicho rectángulo hasta chocar con la columna más chica del histograma.
</details>
<details> 
  <summary>Hint 3</summary>
  <p>El resumen del Hint 2 es que toda query tiene una query equivalente que corresponde a un rectángulo maximal en el "histograma" del arreglo LCP (un rectángulo que no podemos hacer más alto ni más ancho sin salirnos del histograma). Por lo tanto, todos los "searchable subsets" son los archivos distintos que aparecen en el rango de algún rectángulo maximal del arreglo LCP.</p>
  <p>** Hay un caso borde: lo dicho anteriormente es verdad de las querys que hacen match en 2 o más sufijos, ¿pero qué pasa con las queries que hacen match con exactamente un solo sufijo?</p>
</details>
<details>
  <summary>Solución + código</summary>
  En breve: concatenamos todos los files en un puro string. Construimos un suffix array y el arreglo LCP. Vemos el arreglo LCP como histograma y encontramos rectángulos maximales usando un approach de stacks similar al que se usa para resolver <a href="https://www.spoj.com/problems/HISTOGRA/">este problema</a>: basícamente por cada columna i-ésima suponemos que es el techo de un rectángulo maximal, y encontramos los extremos L[i] y R[i] donde comienza y termina el rectángulo. Para obtener los archivos distintos que aparecen en ese rango, podemos usar bitmasks y un sparse table para computar el OR en el rango en O(1), aprovechando el hecho de que son a lo más 60 archivos lo que nos cabe en un long long int (64 bits). Para las queries que hacen match con un solo sufijo, iteramos por todos los sufijos y vemos si LCP[i-1] < len(sufijo[i]) y LCP[i] < len(sufijo[i]). Todos los searchable subsets que encontremos los metemos a un set y finalmente retornamos el tamaño. <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/LiveArchive/5794_FileRetrieval.cpp">Código de ejemplo</a>
</details>

<!-- <details> 
  <summary>Hint</summary>   
</details>
<details> 
  <summary>Solución + código</summary>
  <a href="">Código de ejemplo</a>
</details> -->

[Index](../index) > [Contests](../contests) > [Contest 9](../contests#contest-9) > ```{{page.title}}```
