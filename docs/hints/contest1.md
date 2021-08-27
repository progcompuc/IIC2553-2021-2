---
title: contest 1 - hints y códigos de ejemplo
---

[Index](../index) > [Contests](../contests) > [Contest 1](../contests#contest-1) > ```{{page.title}}```

### A - Largest Rectangle in a Histogram
<details> 
  <summary>Hint</summary>   
  El rectángulo máximo necesariamente tiene una altura igual a alguna columna. Sólo hay N columnas, así que puedes ponerte en los N casos, y sólo te falta saber el ancho. Dada una columna i-ésima, piensa en alguna forma de encontrar los extremos L[i] y R[i] del rectángulo maximal que se formaría si expandimos la columna i-ésima lo más que se puede hacia ambos lados.
</details>
<details> 
  <summary>Solución + código</summary>
  Primero calculamos L[i] de izquierda a derecha (para R[i] podemos hacer lo mismo al revés). Para ello mantenemos un stack, en cada instante el stack guarda los distintos mínimos acumulados de las alturas de las columnas medidos desde la columna i-1 hacia la izquierda, junto con el extremo derecho donde comienza a regir cada mínimo (para entender mejor esto, dibujar un histograma, pararse en alguna columna de al medio y dibujar la altura del mínimo acumulado hacia la izquierda, se ve como una función escalonada). Con ese stack es fácil encontrar L[i] (hacemos pop hasta que llegamos a un mínimo < H[i]) y actualizarlo (pusheamos el par (H[i],i)). Como cada columna es pusheada y popeada sólo 1 vez, la complejidad es O(N). <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/SPOJ/HISTOGRA_LargestRectangleInAHistogram.cpp">Código de ejemplo</a>
</details>

### B - Valeriy and Deque
<details> 
   <summary>Hint</summary>
      Ver si en el algún momento las cosas comienzan a repetirse cíclicamente y aprovechar eso
</details>
<details>
   <summary>Solución + código</summary>
   Simular hasta que el máximo quede al comienzo. De ahí en adelante los que están a la derecha del máximo van rotando. Para las queries que van antes del ciclo responde con lo simulado, y para las queries que caen dentro del ciclo calcula modularmente cual va a ser el elemento sacado. <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/Codeforces/1180C_ValeriyAndDeque.cpp">Código de ejemplo</a>
</details>

### C - Roadwork
<details> 
  <summary>Hint 1</summary>
  Para facilitar el análisis, en vez de pensar para cada persona con qué obstáculo choca, lo podemos ver como para cada obstáculo, qué personas detiene.
  Podemos ver que el obtáculo en X entre S y T detiene a la persona que parte en D si S - X <= D < T - X.
</details>
<details> 
  <summary>Hint 2</summary>
  Si analizamos los obstáculos y las personas en orden temporal (obstáculos tomando tiempo entre los que si una persona sale choca con el) y llevamos cuenta de los intervalos activos, podemos responder la distancia que caminará (en caso de parar) si mantenemos la posición de los obstáculos en una estructura ordenada.
</details>
<details> 
  <summary>Solución + código</summary>
  Podemos generar un vector de eventos temporales el cual recorreremos en orden, los eventos pueden ser, empieza el efecto de un obstáculo (S - X como en Hint 1), termina el efecto de un obstáculo y sale una persona. Al recorrer el vector, basta mantener un multiset ordenado con la posición de los obstáculos que estén activos para poder responder la distancia caminada para cada persona en O(1) cuando salga el evento correspondiente y con updates en O(log N) al empezar o terminar alguno.
  La complejidad total de esta solución es O((N + Q) log(N + Q))
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/AtCoder/Roadwork.cpp">Solución ejemplo</a>
</details>

### D - Two Teams
<details> 
  <summary>Hint 1</summary>
  Podemos ordenar los estudiantes del con mayor habilidad al con menos habilidad podemos agregarlos a un MaxHeap, que agrega elementos en O(log N), consulta por el mayor en O(1) y quita el mayor en O(log N).
</details>
<details> 
  <summary>Hint 2</summary>
  Podemos visitar uno por uno los estudiantes y marcar el equipo correspondiente a los alumnos k a la derecha y a la izquierda no marcados, el problema es que si visitamos muchas veces estudiantes no marcados el algoritmo no cae en el límite de tiempo. Debemos encontrar una forma de no visitar más que una vez cada estudiante. Una estructura perfecta para esto es una lista ligada tal que podamos eliminar segmentos de un arreglo en O(1).
</details>
<details> 
  <summary>Solución + código</summary>
  Recorremos en orden los estudiantes, para cada uno, si no ha sido marcado marcamos k a la derecha y a la izquierda de la lista y eliminamos el segmento.
  Podemos simular la lista ligada usando vectores R, L, tal que R[i] indica qué indice está actualmente a la derecha de i y L[i] a la izquierda de i. al eliminar un segmento sólo debemos unir el de la izquierda del primer eliminado con el de la derecha del último, así en consultas siguientes no se pasará por lo eliminado.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Codeforces/TwoTeams.cpp">Código de ejemplo</a>
</details>

### E - Memory Management
<details> 
  <summary>Hint</summary>
   El problema se puede modelar como una simulación de eventos en el tiempo, desempatando por id. Los bloques libres también se pueden modelar con una estructura que priorice de izquierda a derecha.
</details>
<details> 
  <summary>Solución + código</summary>
  Podemos definir un struct Event para modelar eventos que pueden ser de 3 tipos: memory allocation, memory access y memory release. Los eventos los podemos simular en orden en una priority queue, sacando el siguiente evento del tope dentro de un while. Los eventos de alloc y access son los dados por el input. Los eventos de release los agregamos a medida que vamos simulando y un alloc o access es exitoso. Notar que los release pueden quedar obsoletos (por ej. un access puede extender el periodo de ocupación de un bloque, entonces eventos de release con un timestamp menor ya no son válidos), por lo tanto hay que registrar el último release time por bloque y comparar contra eso para descartar los release obsoletos. A su vez, los bloques de memoria libres se pueden modelar con una priority_queue también (para ir sacando siempre el de más a la izquierda). <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/acm.timus.ru/1037_MemoryManagement.cpp">Código de ejemplo</a>
</details>

### F - Weird Function
<details> 
  <summary>Hint</summary>
  La clave del problema es ordenar los datos de una forma que permita acceder eficientemente a la mediana de estos ordenados.
</details>
<details> 
  <summary>Solución + código</summary>
  Podemos mantener un MaxHeap con la mitad inferior de los datos y un MinHeap con la mitad superior de los datos, tal que podemos acceder a la mediana como el tope del MaxHeap inferior en O(1). Cada vez que agregamos un dato lo agregamos al MaxHeap, si el mayor del MaxHeap es mayor que el menor del MinHeap hacemos un swap de estos datos, y si se desequilibran en tamaño pasamos el mayor del MaxHeap al MinHeap.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/SPOJ/WeirdFunction.cpp">Código de ejemplo</a>
</details>

### G - Criss-cross Cables

<details> 
  <summary>Hint</summary>
  Hay N*(N-1)/2 pares de ubicaciones posibles, que si los ordenamos por largo de menor a mayor codiciosamente nos convendrían los M primeros ¿verdad? Piensa en una forma de encontrar los M primeros sin tener que generar los N*(N-1)/2 pares explícitamente.
</details>
<details> 
  <summary>Solución + código</summary>
  Ordenamos los cables por largo de menor a mayor. Además, usamos un minheap (priority_queue) y primero lo llenamos con intervalos correspondientes a pares consecutivos (i, i+1). Luego de forma sincronizada iteramos sobre los cables y vamos sacando intervalos del minheap, si el algún punto el cable no se la puede o nos quedamos cortos de intervalos, no se puede. Si no, cada vez que sacamos un intervalo, metemos al minheap un nuevo intervalo alargado un índice más a la derecha (o sea, si sacamos el intervalo (i,j), metemos el intervalo (i,j+1)). La complejidad es O(M log M + M log N). <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/kattis/crisscrosscables.cpp">Código de ejemplo</a>
</details>

### H - equeue

<details> 
  <summary>Hint</summary>
   Notar que los límites son chiquitos, así que podemos ponernos en todos los casos de sacar por la izquierda y la derecha.
</details>
<details> 
  <summary>Solución + código</summary>
   Nos ponemos en todos los casos: hacemos dos fors, uno sobre la cantidad de valores que sacamos por la izquierda (L) y otro for sobre la cantidad de valores que sacamos por la derecha (R). Eso define nuestra mano. Luego, con las K-L-R jugadas que nos quedan, codiciosamente las gastamos en botar valores negativos, del más negativo al menos negativo. Eso se puede hacer con una priority_queue. La respuesta va a ser el mejor caso encontrado. <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/AtCoder/abc128_d_equeue.cpp">Código de ejemplo</a>
</details>

### I - Cat Party
<details> 
  <summary>Hint</summary>
  Si pudieramos mantener conteo de las frecuencias de cada color hasta el índice i, este será válido en 3 casos, si todos son del mismo color, si hay un color con frecuencia 1 y todo el resto son iguales o si todos son iguales excepto un color con frecuencia 1 más que el resto. En todos estos casos eliminar 1 funcionaría. Piensen en una forma de mantener frecuencias y poder chequear esos casos eficientemente.
</details>
<details> 
  <summary>Solución + código</summary>
  Si iteramos por índice y mantenemos un multiset ordenado con las frecuencias de cada color que hemos visto podemos chequear todos los casos eficientemente usando iteradores. El primer caso se chequearía viendo si el tamaño del multiset es 1, el segundo caso si el elemento más pequeño del multiset es 1 y el siguiente es igual al último, y el último caso si el último elemento del múltiset es igual al primero - 1 y el primero es igual al penúltimo.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Codeforces/CatParty.cpp">Código de ejemplo</a>
</details>

### J - Who is The Boss
<details> 
  <summary>Hint</summary>
  Podemos ir acumulando la cantidad de subordinados de cada empleado, si todos parten en 0 al ver cual es el jefe los subordinados se le suman.
  Si ordenamos los empleados por salario, todos aquellos empleados ya visitados que no tengan jefe y de altura menor o igual a la del empleado actual serán subordinados y la cantidad de subordinados se acumula. Piensen en una forma eficiente de mantener ordenados los empleados ya visitados sin jefe para hacer eso.
</details>
<details> 
  <summary>Solución + código</summary>
  Si visitamos a los empleados según salario como en el Hint 1, basta mantener un set ordenado o un MinHeap de los empleados ya visitados sin jefe ordenados or altura, luego para cada empleado, agregamos como subordinados a todos aquellos miembros del MinHeap con altura menor o igual a la actual, acumulamos el conteo de subordinados y eliminamos del MinHeap.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/SPOJ/WhoIsTheBoss.cpp">Código de ejemplo</a>
</details>

### K - Daunting Device
<details> 
  <summary>Hint</summary>
  Pensar el problema como intervalos de colores. Inicialmente partimos con un intervalo [0, L-1] pintado todo de color 1, y en cada iteración estamos haciendo una actualización que nos deja una nueva secuencia de intervalos.
</details>
<details> 
  <summary>Solución + código</summary>
  Definimos un struct Interval con 3 variables: índice donde comienza, índice donde termina y color. Además mantenemos un std::set de C++ (un set ordenado) con los intervalos de colores actuales (inicialmente {0, L-1, 1}). Para saber cuántas veces aparece un color, mantenemos un arreglo o vector "freq" (o como quieran llamarle) con las frecuencias de cada color. Luego nos queda implementar el código que ejecuta los N updates. Calculamos M1 y M2 según enunciado. Luego debemos encontrar la secuencia de intervalos en nuestro set que son afectados por el update. Esto se puede hacer usando s.lower_bound() y manipulando iteradores (ver código de ejemplo si te complicas mucho con esto, aunque intenta primero revisar el material del curso sobre sets de C++ y sobre iteradores). Luego podemos borrar todos intervalos con s.erase(), insertar el nuevo intervalo y posiblemente insertar 2 intervalos nuevos en los bordes (si es que nuestro update borra parcialmente algunos de los 2 intervalos vecinos (izquierdo y/o derecho)). Luego de los N updates, la respuesta es el máximo en un nuestro arreglo/vector "freq".  <a href="https://github.com/PabloMessina/Competitive-Programming-Material/blob/master/Solved%20problems/URI/DauntingDevice.cpp">Código de ejemplo</a>
</details>

<!-- <details> 
  <summary>Hint</summary>   
</details>
<details> 
  <summary>Solución + código</summary>
  <a href="">Código de ejemplo</a>
</details> -->

[Index](../index) > [Contests](../contests) > [Contest 1](../contests#contest-1) > ```{{page.title}}```
