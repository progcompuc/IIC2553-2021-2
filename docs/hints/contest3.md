---
title: contest 3 - hints y códigos de ejemplo
---

[Index](../index) > [Contests](../contests) > [Contest 3](../contests#contest-3) > ```{{page.title}}```

### A - Ball
<details> 
  <summary>Hint 1</summary>
  Piensen un una forma de ordenar los datos tal que usando alguna estructura para cada persona podamos saber rápidamente si existe alguien que tenga todas las características mayores.
</details>
<details> 
  <summary>Hint 2</summary>
  Una posible idea es ordenar a las personas de forma decreciente en una de las características (por ejemplo B) e ir manteniendo en una estructura ordenadas según una segunda características (por ejemplo I) las terceras características (por ejemplo R). Piensen cómo mantener esto y en qué estructura ayudaría a saber si hay alguien dominante rápidamente.
</details>
<details> 
  <summary>Solución + código</summary>
  Siguiendo la idea del hint 2, recorriendo de forma decreciente en una de las características podemos mantener un Segment Tree donde el índice indica el orden en la 2a característica y los valores corresponden a la 3a característica. De esta forma con un query de máximo al segmento (i, end) donde i corresponda a uno más que el valor de la persona que se revisa actualmente, si el mayor valor es mayor que el valor de la 3a característica actualmente entonces debe haber una persona con mayores valores en cada característica.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Codeforces/Ball.cpp">Código de ejemplo</a>
</details>

### B - D-query
<details> 
  <summary>Hint</summary>
  Piensa en una forma de ordenar las queries, de tal manera que al ir iterando sobre ellas puedas ir actualizando una estructura de datos que te permita contar cuántos números están activos (teniendo cuidado de nunca activar números duplicados simultáneamente).
</details>
<details> 
  <summary>Solución + código</summary>
  Lo que hacemos es ordenar las queries (L,R) de forma creciente en R. Además, creamos un fenwick tree de tamaño N en el cual vamos trackeando con 0s y 1s los números del arreglo actualmente activos (inicialmente partimos con puros 0s, i.e. ningún número activo). Luego vamos iterando sobre las queries (crecientes en R) y para cada query hacemos avanzar un puntero r hasta alcanzar el R actual, y en cada paso activamos el número r-ésimo (sumamos 1 en la posición r-ésima del fenwick tree, indicando que el número r-ésimo está activo), <strong>PERO</strong> si el número r-ésimo ya estaba activo en una posición anterior, lo desactivamos (sumamos -1 en su posición anterior). De esta manera si un número está duplicado, siempre mantenemos activa la posición más a la derecha en la que aparece. Con eso logramos que se cumpla la invariante de que de todos los distintos números dentro del intervalo [1,R] estén activados en sus respectivas posiciones más a la derecha (dentro de [1,R]), y todo el resto está desactivado. Luego, para saber cuántos números distintos hay consultamos al fenwick tree la suma acumulada de 1s en el intervalo [L,R]. <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/SPOJ/DQUERY_D-query.cpp">Código de ejemplo</a>
</details>
<details> 
  <summary>Solución Alternativa + código</summary>
  El problema se puede hacer trivialmente también aplicando el <a href="../resources/sqrtdecomp">algoritmo de MO</a>. <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/SPOJ/DQUERY_D-query_v2.cpp">Código de ejemplo</a>
</details>

### C - Vladik and Entertaining Flags
<details> 
  <summary>Hint 1</summary>
  Piensa en una forma de responder la query(L,R) descomponiendo el rango [L,R] en sub-rangos y combinando respuestas precomputadas para dichos sub-rangos.
</details>
<details>
  <summary>Hint 2</summary>
  Supón que tienes la respuesta precomputada para el rango [L,M] y para el rango [M+1, R]. ¿Cómo obtener la respuesta para el rango [L, R]? Notar que las componentes de ambos rangos se fusionan si es que en el punto de contacto entre las columnas M y M+1 hay valores adyacentes iguales. Cualquier componente que no toque la interfaz no se puede fusionar.
</details>
<details> 
  <summary>Solución + código</summary>
  Básicamente usamos ya sea un Sparse Table o un Segment Tree, los rangos los modelamos con un Struct/Class que guarde los índices L y R del rango, un par de arreglos int left[10] e int right[10] que guarden los ids de las componentes a las que pertenecen los valores de las columnas L y R respectivamente, y un contador de la cantidad de componentes del rango. Para fusionar los rangos A = [L, M] y B = [M+1, R], podemos iterar sincronizadamente sobre las columnas M y M+1 y detectar cuando los valores matrix[M][i] == matrix[M+1][i], en cuyo caso las componentes A.right[i] y B.left[i] deben fusionarse (podemos iterar sobre las 4 columnas A.left, A.right, B.left y B.right y actualizar los ids). Usando Sparse Table la complejidad es O(N^2*M*log(M)) por construir el sparse table y O(Q*N^2*log(M)) por responder las queries. <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/Codeforces/811E_VladikAndEntertainingFlags_v2.cpp
">Código de ejemplo</a>
</details>

### D - Update the array!
<details> 
  <summary>Hint</summary>
  Podemos construir un arreglo D de que guarde las diferencias que generan los updates, en otras palabras, si se hace un update l, r, v, realizamos D[l] += v, D[r + 1] -= v. Luego pensar en una forma de rescatar el valor en un índice de forma rápida, luego de los updates y usando el arreglo D.
</details>
<details> 
  <summary>Solución + código</summary>
  Una forma de resolver este problema de forma online, podemos hacer uso del arreglo de diferencias descrito en el hint y generar un segment tree de el que calcule la suma en un rango. Luego se recupera el valor en un índice realizando queries de la forma (0, i) a la estructura.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/SPOJ/UpdateTheArray.cpp">Código de ejemplo</a>
</details>

### E - Range Minimum Query
<details> 
  <summary>Hint</summary>
  Problema de uso directo de alguna de las estructuras vistas en clases
</details>
<details> 
  <summary>Solución + código</summary>
  Puede ser resuelto con uso directo de Segment Tree o Sparse Tables.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/SPOJ/RangeMinimumQuery.cpp">Código de ejemplo</a>
</details>

### F - Gravel
<details>
  <summary>Hint 1</summary>
  Este problema es similar al B - update the array, tenemos updates sobre rangos y consultas puntuales. La diferencia es que acá los updates y consultas pueden estar intercalados.
</details>
<details>
  <summary>Hint 2</summary>
  Al igual que en el problema B - update the array, podemos usar el concepto de <a href="https://www.geeksforgeeks.org/difference-array-range-update-query-o1/">difference array</a>, sin embargo, como acá tenemos updates y consultas intercalados, recalcular un difference array a cada rato daría TLE. ¿Se te ocurre alguna forma de implementar el mismo concepto de difference array pero con una estructura que permita hacer updates y consultas de forma eficiente?
</details>
<details>
  <summary>Solución + código</summary>
  Usamos un fenwick tree (a.k.a. bit) para simular un difference array dinámico. Cuando nos piden hacer un update por rango, hacemos bit.add(l,k) y bit.add(r+1,-k), y cuando nos hacen una consulta puntual consultamos con bit.psq(p). La complejidad es O(M log N). <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/Codechef/SPREAD_Gravel.cpp">Código de ejemplo</a>
</details>

### G - Xenia and Bit Operations
<details> 
  <summary>Hint</summary>
  Pinesen en cómo construir un nodo para poder resolver el problema con un Segment Tree
</details>
<details> 
  <summary>Solución + código</summary>
  Si en cada nodo guardamos el valor y la profundidad inversa (empezando desde 0 en las hojas), podemos realizar distintas operaciones en la unión de dos nodos dependiendo de la profundidad en la que se produzca la unión, es decir, si la profundidad es par unimos con or y si es impar unimos con xor. Ambas operaciones son compatibles con un Segment Tree y la complejidad final es O(m log(2^n)). Ojo que para que de accepted tal vez sea necesario el uso de fast input en c++.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Codeforces/XeniaAndBitOperations.cpp">Código de ejemplo</a>
</details>

### H - Cut Inequality Down
<details> 
  <summary>Hint 1</summary>
  Si estamos parados en el mes B con un ingreso inicial de X (L <= X <= U), si dibujamos la curva de nuestro ingreso acumulado mensual mes a mes (X + la sumatoria de los A hasta el mes actual) ignorando las cotas U y L, notaremos que la curva a veces choca con la cota L y a veces con la cota U. Notar que el instante que nos interesa encontrar es el primer choque (el mes del choque y con cuál de las 2 cotas chocamos). De ahí en adelante el proceso se puede pensar como ir saltando de choque en choque, hasta llegar al último choque que no se pase del mes E. Desde ese punto hasta E no hay choques, así que ahí es fácil calcular el dinero total en el mes E.
</details>
<details> 
  <summary>Hint 2</summary>
  Si estamos en el mes B con un ingreso inicial de X, ¿cómo podemos encontrar el mes y la cota del siguiente choque? Una forma de verlo es pensar en una estrategia para encontrar el primer choque con cada cota (U y L) suponiendo que la otra cota no existe, y el primero de los dos que ocurra es el siguiente choque.
</details>
<details> 
  <summary>Hint 3</summary>
  Si para cada par (i, cota) tenemos precomputado el siguiente choque (i', cota'), la query (X, B, E) se podría resolver de la siguiente manera: primero encontrar el primer choque, si ocurre pasado de E, entonces no hay choques entre B y E y el cálculo es trivial, si hay choque, entonces nos paramos en el choque (i, cota) y seguimos los punteros al siguiente choque (i', cota') y así sucesivamente hasta llegar al último choque <= E, y luego ahí es trivial calcular el dinero final. El problema de esto es que en el peor caso podría pasar que hay que seguir muchos punteros y eso podría dar TLE. Piensa en una forma de optimizar este proceso, quizás precomputando saltos exponenciales de punteros.
</details>
<details> 
  <summary>Solución + código</summary>
  Para cada mes i y cota (U o L) precomputamos el siguiente choque (i', cota'). Esto se puede hacer con dos búsquedas binarias que en el predicado usen un sparse table de máximo o mínino sobre un arreglo accA (los ingresos de A acumulados). Para pegarnos saltos exponenciales, podemos crear un tercer sparse table que implemente <a href="https://youtu.be/kOfa6t8WnbI?t=405">binary lifting</a> sobre los punteros obtenidos anteriormente. Para responder las Q queries (X,B,E) podemos hacer una búsqueda binaria inicial para encontrar el primer choque, luego hacer binary lifting para encontrar el último choque que no se pasa de E, y luego cálcular el último cachito hasta E en O(1) haciendo restas de sumas acumuladas. <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/Matcomgrader/CutInequalityDown.cpp">Código de ejemplo</a>
</details>


<!-- <details> 
  <summary>Hint</summary>   
</details>
<details> 
  <summary>Solución + código</summary>
  <a href="">Código de ejemplo</a>
</details> -->

[Index](../index) > [Contests](../contests) > [Contest 3](../contests#contest-3) > ```{{page.title}}```
