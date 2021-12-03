---
title: contest 11 - hints y códigos de ejemplo
---

[Index](../index) > [Contests](../contests) > [Contest 11](../contests#contest-11) > ```{{page.title}}```

### C - Dazzling Stars
<details> 
  <summary>Hint 1</summary>
  Se puede reinterpretar como ver si existe un vector (o dirección con sentido) donde al proyectar las estrellas nunca aparezca una estrella de mayor brillo antes que una de menor brillo. Siempre existirá esta dirección si los vectores que van de estrellas de menor brillo a mayor brillo no son incompatibles.
</details>
<details> 
  <summary>Hint 2</summary>   
  Si ordenamos los vectores que van de menor a mayor brillo por ángulo, serán compatibles si existe un rango de 180 que los contiene a todos.
</details>
<details> 
  <summary>Solución + código</summary>
  Basta hacer un sweepline radial con eventos de inicio y final de rango para cada vector. Si tenemos un vector v, agregaremos sus rotaciones en +- 90 grados al sweepline como inicio y fin de rango. Si al recorrer los eventos en orden en algún momento todos los rangos están activos la respuesta será Y.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/Matcomgrader/DazzlingStars.cpp">Código de ejemplo</a>
</details>

### E - Balloon
<details>
  <summary>Hint 1</summary>
  Cada segmento si es inclinado libera globos o hacia otro segmento o hacia el vacío, esto forma un DAG (directed acyclic graph) de los segmentos sobre el cual podemos aplicar programación dinámica para encontrar la solución al problema. Piensen en cómo armar el dag usando un sweepline sobre eventos ordenados por eje x con eventos inicio de segmento, fin de segmento y globo.
</details>
<details>
  <summary>Hint 2</summary>
  Si usamos un sweepline como descrito y mantenemos un set ordenado con los segmentos activos podremos armar el DAG. Para mantener los segmentos ordenados basta usar un comparador de pares de segmentos y usar un set. Dados dos segmentos AB y CD si A.x > C.x entonces AB estará bajo CD si CA x XD < 0.
</details>
<details>
  <summary>Hint 3</summary>
  Podemos armar el dag uniendo cada al segmento que va justo más arriba en el set, esto se define al momento de agregar el segmento si está inclinado hacia la izquierda o al momento de eliminarlo si está inclinado hacia la derecha (Pueden usar upper_bound en c++ para buscar el siguiente segmento). También debemos recordar el menor segmento del set en cada evento globo, pues será el primero con que choca el globo (la respuesta de este globo será evaluar el dp en el segmento con que chocó primero).
</details>
<details>
  <summary>Solución + código</summary>
  Dado el DAG descrito en los hints basta armar un algoritmo de programación dinámica que resuelve el problema. Cada segmento busca la respuesta en el segmento al que apunta, en caso de apuntar a un segmento no inclinado se queda en esa posición y en caso contrario se sigue preguntando.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/URI/Balloon.cpp">Código de ejemplo</a>
</details>
  
### G - Garden Fence
<details> 
  <summary>Hint 1</summary>
  Notemos que a menos que el óptimo sea dejar todos los árboles a un lado, la solución siempre será una recta que separa dos árboles de cada tipo. De hecho se puede mostrar que el óptimo siempre puede ser alcnzado con una rotación infinitesimal de alguna recta que una dos árboles de cada tipo. Piensen en una forma de recorrer todas las rectas uniendo árboles de tipos distintos considerando el costo de elegirla (en una rotación infinitesimal).
</details>
<details> 
  <summary>Hint 2</summary>
  Podemos considerar todas estas en tiempo rectas realizando P sweeplines radiales desde cada árbole de tipo P. Usando dos punteros sobre el orden de un sweepline radial de un árbol de tipo P es posible acumular y actualizar el costo en tiempo amortizado O(n). Basta acumular cada vez que se avanze el puntero de un rango de 180 el segundo puntero hasta el final del rango. Luego de hacer todos los sweepline, la instancia de menor costo será la respuesta.
</details>
<details> 
  <summary>Solución + código</summary>
  Basta implementar los hints. Tener cuidado con puntos colineales, en caso de empate en el sweepline radial siempre conviene usar primero el punto a menor distancia y saltarse el resto para el sweepline (igual deben ser acumulados para el costo).
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/URI/GardenFence.cpp">Código de ejemplo</a>
</details>
  
### H - Hide and seek
<details> 
  <summary>Hint 1</summary>
  Piensen en como hacer un sweepline radial desde cada seeking kid donde hayan eventos de comienzo de pared, fin de pared y hiding kid. En el sweepline deben mantener ordenadas las paredes activas en orden de distancia al seeking kid.
</details>
<details>
  <summary>Hint 2</summary>
  Ordenar los eventos de cada sweepline se hace de forma estándar, la dificultad de este problema radica en el orden de los segmentos activos durante el sweepline. Un posible comparador para usar un set para el orden puede ser, dados dos segmentos activos AB y CD, si A empieza después que C entonces A será menor si CA x CD > 0 (producto cruz).
</details>
<details>
  <summary>Solución + código</summary>
  Dado el sweepline explicado en los hints siempre que un evento hiding kid tenga posición menor a todos los segmentos activos (basta comparar con el más cercano), entonces será visible desde el seeking kid analizado.
  <a href="https://github.com/BenjaminRubio/CompetitiveProgramming/blob/master/Problems/URI/HideAndSeek.cpp">Código de ejemplo</a>
</details>

<!-- <details>
  <summary>Hint</summary>
</details>
<details>
  <summary>Solución + código</summary>
  <a href="">Código de ejemplo</a>
</details> -->

[Index](../index) > [Contests](../contests) > [Contest 11](../contests#contest-11) > ```{{page.title}}```
